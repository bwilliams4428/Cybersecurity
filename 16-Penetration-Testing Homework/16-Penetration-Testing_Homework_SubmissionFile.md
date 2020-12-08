## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:
	
	**The Chief Executive Officer for Altoro Mutual is Karl Fitzgerald.**
	
	**Using the Google Dork  "site:demo.testfire.net intext:Chief Executive Officer", returned two results which reveals the CEO of Altoro 		Mutual:**
		http://demo.testfire.net/pr/communityannualreport.pdf
		http://demo.testfire.net/index.jsp?content=pr/20060720.htm
	
	**Using the dork "intext:altoro Chief Executive Officer" produces the page that lists Altoro Mutuals executives and managers:**
		http://www.altoromutual.com/index.jsp?content=inside_executives.htm
	
- How can this information be helpful to an attacker:
	
	**This information can be used in a spear phishing and social engineering campaigns against the CEO. An attacker may also be able to find  	   other sources of data associated with the CEO such as personal social media accounts, home address, family members and criminal records.**
	
#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located: 
		
		**Sunnyvale, California** 
  
  2. What is the NetRange IP address:
		
		**65.61.137.64 - 65.61.137.127**
		
  3. What is the company they use to store their infrastructure:
		
		**Rackspace Backbone Engineering**
		
  4. What is the IP address of the DNS server:
		
		**65.61.137.117, but I have a reservation about this answer.**
		
		**65.61.137.117 is IP for the web server that demo.testfire.net uses. The nameservers (ns records) that testfire.net provides DNS 		  server information:**
		```
		dig ns testfire.net
		; <<>> DiG 9.16.2-Debian <<>> ns testfire.net
		;; global options: +cmd
		;; Got answer:
		;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2765
		;; flags: qr rd ra; QUERY: 1, ANSWER: 8, AUTHORITY: 0, ADDITIONAL: 1

		;; OPT PSEUDOSECTION:
		; EDNS: version: 0, flags:; udp: 512
		;; QUESTION SECTION:
		;testfire.net.                  IN      NS

		;; ANSWER SECTION:
		testfire.net.           21599   IN      NS      ns1-206.akam.net.
		testfire.net.           21599   IN      NS      asia3.akam.net.
		testfire.net.           21599   IN      NS      eur2.akam.net.
		testfire.net.           21599   IN      NS      usc2.akam.net.
		testfire.net.           21599   IN      NS      usw2.akam.net.
		testfire.net.           21599   IN      NS      ns1-99.akam.net.
		testfire.net.           21599   IN      NS      usc3.akam.net.
		testfire.net.           21599   IN      NS      eur5.akam.net.

		;; Query time: 76 msec
		;; SERVER: 192.168.1.1#53(192.168.1.1)
		;; WHEN: Tue Dec 08 00:54:20 EST 2020
		;; MSG SIZE  rcvd: 204
		```
		

#### Step 3: Shodan

- What open ports and running services did Shodan find:
	
	**Ports 80, 443 and 8080 were open on the server's IP. The Apache Tomcat webserver was the only service running on the server.**
	![Image of Shodan](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/16-Penetration-Testing%20Homework/images/16Penshodan.PNG)

#### Step 4: Recon-ng

- Install the Recon module `xssed`. 
- Set the source to `demo.testfire.net`. 
- Run the module. 

Is Altoro Mutual vulnerable to XSS: 
	
   Yes, Altoro Mutual is vulnerable to XSS. An XSS vulnerability was discovered on 08/02/2009.
	
   ![Image of Recon-ng](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/16-Penetration-Testing%20Homework/images/recon-ng2.PNG)
   ![Image of Recon-ng](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/16-Penetration-Testing%20Homework/images/recon-ng1.PNG)


### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine: 
		
		nmap -sV 192.168.0.10

- Bonus command to output results into a new text file named `zenmapscan.txt`:
		
		nmap -sV -oS zenmapscan.txt 192.168.0.10
	
- Zenmap vulnerability script command: 

		nmap -TF -F --script smb-enum-shares,smb-os-discovery 192.168.0.10
		

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:
		
		My scan discovered two vulnerabilities affecting service message block(SMB):
			
			smb-enum-shares - Lists the shares that use the SMB protocol on the targeted system. It provides other information about the shares
							  such as the username, path and if anonymous access is enabled.
			
			smb-os-discovery - Provides information about the targeted system over SMB protocol. Information such as the operating system, the system's hostname, workgroup
							   and system time.
		
  2. Why is it dangerous:
			
			An attacker can use smb-enum-shares to find sensitive data being shared via SMB and writeable directories for an attacker to place trojans.
			
			An attacker can use the information generated from smb-os-discovery to determine the types of attacks to wage against the target based on the operating system.

  3. What mitigation strategies can you recommendations for the client to protect their server:
			
			Have all directories that are shared using SMB protocol be password protected and disable anonymous access for shares.
			
			Disable SMB v1 and use SMB v2.
			
---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

