# Brief overview
This project contains 3 virtual machines: a machine that runs Windows Server, one that runs Windows Client and the last one running Ubuntu. The alterations made in each VM is thoroughly described in this file. <br/>
Each VM has been uploaded to OneDrive, since they are large files that cannot be directly uploaded to GitHub. You can access the folder that contains the VMs [here](https://1drv.ms/f/s!AiJja_jxQJ8ggcEzTFktyAXqb-zKIA?e=uXwwhq).<br/>


# How to run
- CHECK THE CREDENTIALS FILE !!!!!!!------------------------------


# Functionalities

## Windows Server (WS) and Windows Client (WC)

### Making sure they connect
Before we start doing anything else, you need to first make sure that our VMs work properly and are interconnected. In order to do so, you need to follow these steps:
- power both machines up (they need to be on at the same time)
- login with
	- the admin user on WS
 	- proiectso on WC
- disable all firewall options on both machines

After having done all that, open Command Prompt on both machines and type:
- In WS: ping 192.168.250.1
- In WC: ping 192.168.250.2

If you don't see any package loss, then congratulations! It works and you may now proceed further.


### Windows Server

#### Domain
The server's domain name is domeniu.local and both the client and the server are in that domain.

#### Users and groups
There are 3 users and 2 groups created:
- user1 and user2 are in group1
- user2 and user3 are in group2

#### Block access to control panel (GPE)
There is a policy set on WS that blocks the access to control panel for the users. In order to see the implementation of the rules, follow these steps from Windows Server: **tools -> group policy editor -> forest -> domains -> domeniu.local**
Once you are here, you will see 2 created rules:
- disable task manager
- no control panel
The first rule disables task manager for group1 and the second disables control panel for group2.

#### File transfer
In order to change rwx (read, write, execute) permissions for a shared file within the domain, you need to follow these steps: 
- open Computer Management -> system tools -> shared folders -> shares -> propersties of sf1 -> share permissions
Once you got here, you may now change the folder's permissions. You can do so for any file you create here, which you can do by simply pressing right click on the blank space, select new share and then you can make your own configuaration for the file.


### Windows Client
#### Users and groups
As iterated in the WS section, we found out that there are 3 users and 2 groups created. However, there is another user that I have not talked about yet, which is proiectso. This user was the one who was originally connected <br/>
I will remind you that you can find the credentials for the users in the credentials.md file. 

#### Group Policy Editor
Apart from the policy set from WC for the groups, I have also set a local firewall rule in proiectso, which you will need to enable and then disable yoruself after you are done with testing it. In order to find the policy, you need to navigate to: **Group Policy Editor -> user configuration -> administrative templates -> control panel -> prohibit access to control panl -> tick enabled**.<br/>
Once you have done that, the access to control panel should be prohibited. In order to disable it, simply untick the enabled box.

#### Task Scheduler:
Another implemented functionality is a scheduled task. The chosen automation is opening notepad when the clock reaches a certain time. In order to test this, you will need to set the time yourself to an upcoming moment. <br/>
In order to do so, 


Task Scheduler:
- task scheduler -> task scheduler library -> open notepad -> properties
	- ii aratam setarile e care le-am facut la conditions
		- untick start the task only if the computer is on ac power
	- set an upcoming time

Script:
- script.bat -> run
- ii aratam in fisierul script.txt script-ul folosit pentru a crea folderul


Firewall rule:
- control panel -> windows defender firewall -> advanced settings -> inbound rule -> block self connection -> enabled
- enable firewall
- check if it works: Windows Server -> cmd -> ping 192.168.250.1
- disable the rule
- disable firewall

### Ubuntu


-------------------------------------------------------------------------------------------------------
WINDOWS SERVER:









UBUNTU:
SSH:
- putty

Users:
- switch to user 1

VSFTPD / ftp:
- ftp 

Samba:
- ii dau drepturi de add si remove files !!!!!!!

Firewall:
- sudo ufw
	- enable
	- allow 22
	- status
	- deny 22
	- disable

Server mail:
- switch to chatgpt
- bard@vaibhav.com

Site / virtual host:
- http://site1.com
