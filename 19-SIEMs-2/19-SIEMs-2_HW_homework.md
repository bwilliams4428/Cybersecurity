## Brian C Williams

## Unit 19 Homework: Protecting VSI from Future Attacks

### Scenario

In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks. 

You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

### System Requirements 

You will be using the Splunk app located in the Ubuntu VM.

### Logs

Use the same log files you used during the Master of SOC activity:

- [Windows Logs](resources/windows_server_logs.csv)
- [Windows Attack Logs](resources/windows_server_attack_logs.csv)
- [Apache Webserver Logs](resources/apache_logs.txt	)
- [Apache Webserver Attack Logs](resources/apache_attack_logs.txt	)

---

### Part 1: Windows Server Attack

Note: This is a public-facing windows server that VSI employees access.
 
#### Question 1
- Several users were impacted during the attack on March 25th.
- Based on the attack signatures, what mitigations would you recommend to protect each user account? Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.
   
 **According to the windows server attack logs, the signatures that had outstanding suspicious activity on March 25th are:**
 
 * **User account was locked out (Most affected user: A)**
 * **An attempt was made to reset a user’s password (Most affected user: K)**
 * **An account was successfully logged on (Most affected user: J)**
 
 **Global mitigation strategies:**
 
 * **Require all users to use two factor authentication when logging in** 
 * **Only accept logins attempts to the company’s website from connections made from a VPN or proxy server that was approved**
 * **Only accept login attempts from connections made from whitelisted IPs**
 * **Block IPs that make a high volume of failed login attempts within a short period of time**

 **Individual mitigation strategies:**
 
 * **The threat actor attempted to access User A’s account using a brute force attack causing the account to lock. User A will need reset the password for the account. User A must use a strong password that is not similar to the last password used. Once the password has been changed, the system/server admin may need to reset the lockout the timer so that User A is able to login using the new password.**
 * **The threat actor made multiple attempts to reset User K’s password. The threat actor was not successful in changing the password. User K’s account will need to be monitored for password reset attempts. If the account experiences a high volume of password reset attempts then the IP(s) that the password reset attempts originated from will be blocked. User K will be required to reset the password for their account.**
 * **The threat actor was able to access User J’s account. User J’s account will need to be reset. Require User J to use two factor authentication when accessing the account. Another consideration would be to terminate the account and create a new account for User J with a different username.**

#### Question 2
- VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.
- What sort of mitigation could you use to protect against this?
   
   * **VSI can inform its users that to treat unsolicited login information that they receive as spam and to delete such messages.**
   * **Set the account lockout timer to expire in 10-15 minutes so that users affected by are able to login in a timely manner. The user will be forced to changed to the account’s password once the lockout has expired.**
  

### Part 2: Apache Webserver Attack:

#### Question 1
- Based on the geographic map, recommend a firewall rule that the networking team should implement.
- Provide a "plain english" description of the rule.
  - For example: "Block all incoming HTTP traffic where the source IP comes from the city of Los Angeles."
      
      **The logs show a high volume of suspicious activity originating from cities Kyiv and Kharkiv in the Ukraine. The attacker tried brute force access to VSI user accounts since the threat actor accessed /VSI_Account_login.php. A firewall rule to block traffic in those cities is:**
      
   * **Block all incoming HTTP traffic to VSI_Account_login.php where source IP equal 194.105.145.147(Kyiv) or 79.171.127.34(Kharkiv)**

- Provide a screen shot of the geographic map that justifies why you created this rule. 
![Image of map](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/19-SIEMs-2/images/map.PNG)
![Image of map](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/19-SIEMs-2/images/County.PNG)
![Image of map](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/19-SIEMs-2/images/City.PNG)


#### Question 2

- VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

- What other rules can you create to protect VSI from attacks against your webserver?
  - Conceive of two more rules in "plain english". 
  - Hint: Look for other fields that indicate the attacker.
   
   * **Block all incoming POST requests to VSI_Account_login.php where region equals Kyiv City or region equals Kharkivs'ka Oblast'**
   * **Block all incoming POST requests to VSI_Account_login.php where country equals Ukraine**
   * **Block all incoming POST requests to VSI_Account_login.php where bytes equal 65748 and country equals Ukraine**

 
