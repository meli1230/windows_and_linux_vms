# Brief overview
This project contains 3 virtual machines: a machine that runs Windows Server, one that runs Windows Client and the last one running Ubuntu. Each VM has been uploaded to OneDrive, since they are large files that cannot be directly uploaded to GitHub. The link to each VM will be provided in the next block. <br/>


# Links:
- [Windows Server 2022](https://1drv.ms/u/s!AiJja_jxQJ8ggcEwll38qT2MzAKr7g?e=Pkzo33)
- [Windows 10 Pro (client)](https://1drv.ms/u/s!AiJja_jxQJ8ggcExgBdDiV4oxcC1Pw?e=YVAN1b)
- [Ubuntu 24.04](https://1drv.ms/u/s!AiJja_jxQJ8ggcEv0frjZymaAmBMww?e=VUducP)


# How to run
- CHECK THE CREDENTIALS FILE !!!!!!!------------------------------


# Functionalities

## Windows Server (WS) and Windows Client (WC)

### Making sure they connect
Before we start doing anything else, you need to first make sure that our VMs work properly and are interconnected. In order to do so, you need to power both machines up (they need to be on at the same time), open Command Prompt on both and write the follwoing commands:
- In WS: ping 192.168.250.1
- In WC: ping 192.168.250.2

If you don't see any package loss, then congratulations! It works and you may now proceed further.


### Windows Server

##### Domain
The server's domain name is domeniu.local and both the client and the server are in that domain.

##### Users and groups
There are 3 users and 2 groups created:
- user1 and user2 are in group1
- user2 and user3 are in group2

##### Block access to control panel
There is a policy set on WS that blocks the access to control panel for the users. In order to activate it, if it is not already active, follow the steps from the Server Manager window: **tools -> group policy editor -> forest -> domains -> domeniu.local**
Here

Group Policy Editor:
- tools -> gpe -> forest -> domains -> domeniu.local -> 
	- disable task manager -> ii aratam a avem
	- no control panel -> ii aratam a avem


IIS & DNS
- ii aratam site-urile din IIS & DNS din Server Manager


File Trasnfer:
- computer management -> shared folders -> shares -> properties sf1 -> share persmissions

### Windows 10 Pro


### Ubuntu


-------------------------------------------------------------------------------------------------------
WINDOWS SERVER:






WINDOWS CLIENT:
Firewall:
1. disable firewall & check ping to client

2. continue here
	- enable firewall
	- cmd -> ping 192.168.250.2

3. disable firewall


Group Policy Editor:
- gpe -> user configuration -> administrative templates -> control panel -> prohibit acces to control panel and pc settings -> enabled 
- dupa, dam disable inapoi
- verificam ca merge acum control panel


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
