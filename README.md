# Brief overview
This project contains 3 virtual machines: a machine that runs Windows Server, one that runs Windows Client and the last one running Ubuntu. Each VM has been uploaded to OneDrive, since they are large files that cannot be directly uploaded to GitHub. The link to each VM will be provided in the next block. <br/>


# Links:
- [Windows Server 2022]()
- [Windows 10 Pro (client)]()
- [Ubuntu 24.04]()


# Functionalities
## Windows Server
##### Users and groups
- there are 3 users and 2 groups creaed
- user1 and user2 and in group1, while user2 and user3 and in group2

##### Firewall
  



## Windows 10 Pro


## Ubuntu


-------------------------------------------------------------------------------------------------------
WINDOWS SERVER:
Users & groups:
- Tools -> acrive directory users and computers -> users


Firewall:
1. disable firewall & check ping to client

2. on the spot:
	- enable firewall
	- control panel -> windows defender firewall -> advanced settings -> inbound rules -> 192.168.250.1 blocked -> properties -> enabled -> ok
	- go to client 

3. disable firewall


Group Policy Editor:
- tools -> gpe -> forest -> domains -> domeniu.local -> 
	- disable task manager -> ii aratam a avem
	- no control panel -> ii aratam a avem


IIS & DNS
- ii aratam site-urile din IIS & DNS din Server Manager


File Trasnfer:
- computer management -> shared folders -> shares -> properties sf1 -> share persmissions



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