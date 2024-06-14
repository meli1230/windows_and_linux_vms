# Brief overview
This project contains 3 virtual machines: a machine that runs Windows Server, one that runs Windows Client and the last one running Ubuntu. The alterations made in each VM is thoroughly described in this file. <br/>
Each VM has been uploaded to OneDrive, since they are large files that cannot be directly uploaded to GitHub. You can access the folder that contains the VMs [here](https://1drv.ms/f/s!AiJja_jxQJ8ggcEzTFktyAXqb-zKIA?e=uXwwhq).<br/>


# How to run
- CHECK THE CREDENTIALS FILE !!!!!!!------------------------------
- talk about escape key ------------------------------------!!!!


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
There is a policy set on WS that blocks the access to control panel for the users. In order to see the implementation of the rules, follow these steps from Windows Server: *tools -> group policy editor -> forest -> domains -> domeniu.local*. <br/>
Once you are here, you will see 2 created rules:
- disable task manager
- no control panel
The first rule disables task manager for group1 and the second disables control panel for group2.

#### File transfer
In order to change rwx (read, write, execute) permissions for a shared file within the domain, you need to follow these steps: 
- open Computer Management -> system tools -> shared folders -> shares -> propersties of sf1 -> share permissions

Now you may now change the folder's permissions. You can do so for any file you create here, which you can do by simply pressing right click on the blank space, select new share and then you can make your own configuaration for the file.


### Windows Client
#### Users and groups
As iterated in the WS section, we found out that there are 3 users and 2 groups created. However, there is another user that I have not talked about yet, which is proiectso. This user was the one that was used to make the domain connection between WS and WC. I will remind you that you can find the credentials for the users in the credentials.md file. 

#### Group Policy Editor
Apart from the policy set from WC for the groups, I have also set a local firewall rule in proiectso, which you will need to enable and then disable yoruself after you are done with testing it. In order to find the policy, you need to navigate to: *Group Policy Editor -> user configuration -> administrative templates -> control panel -> prohibit access to control panl -> tick enabled*. Once you have done that, the access to control panel should be prohibited. In order to disable it, simply untick the enabled box.

#### Task Scheduler:
Another implemented functionality is a scheduled task. The chosen automation is opening notepad when the clock reaches a certain time. In order to test this, you will need to set the time yourself to an upcoming moment.
In order to do so, you will need to follow these steps: *open Task Scheduler -> task scheduler library -> open notepad -> properties -> triggers*. When you got here, set the time to your liking and then wait until the clock reaches that value. When that happens, notepad should open automatically.

#### Script:
You may have noticed two files on the desktop already: *script.bat* and *script.txt*. Click the *script.bat* file and see what it does. <br/>
As you have probably noticed, the script created a folder on Desktop, that contains a textfile with some writing in it. 
<br/>In order to see how that was done, open *script.txt*, which contains the same script that was used to automate the folder and file creation you just saw.


### Ubuntu
#### Making the machine run properly
Before jumping into the functionalities that I have implemented, you need to make a few changes in a file, in order to make sure that the IP address used in it is the same as the one of the VM. What you need to modify is located in etc/hosts, which you can reach by typing the follow these steps: 
- open Terminal and type *ipconfig*- in the returned result, search for inet, which should be followed by your ip address
- the next command we need to type in the terminal is *sudo nano /etc/hosts*
Once you opened this file, you need to replace every ip address you see with your ip address, which you have just discovered by using *ifconfig*. When done, press ctrl+x to save the file and then enter to exit.

#### SSH Putty
The first thing that I installed on my virtual machine is SSH, which stands for Secure Shell. This a protocol that will let use an app like putty to remotely connect to our virtual machine from any other machine, regardless of the native operating system. To test putty you need to first install the app on your physical machine or on any other machine you would like. You can use [this link](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) to simply get an exe file, from the *Alternative binary file* section.<br/><br/>
Once it downloaded, open *putty.exe*. In the window that just opened, make sure that *Port 22* is selected, as well as *Connection type: SSH* and, after that, write the IP address of the Ubuntu VM in the *Host Name (or IP address) section*. If you have done that correctly, a terminal-like window should pop up, requesting a username and password. <br/><br/>
Use the credentials provided in the *credentials.md* file and be weary of the fact that whenever you type the password, characters are being written down without anything being shown on screen, so you are typing, even if you don't have any feedback to confirm that.<br/>
You may now continue to use putty in the same way you would use the Terminal on the VM.

#### Users
In order to switch between users in the terminal, use the command *su user_name*. For example, to switch to user1 we would write *su user1*.

#### VSFTPD
Ftp, also known as file transfer protocol, is a daemon used to easily transfer files between Windows and Linux. Ftp is already installed on the VM, so all you have to do is use it. Before proceeding further, we assume that a file *c.txt* is already created in Ubuntu and another one, named *d.txt* is created in Windows. After making sure that those files exist, follow these steps:
- Linux Terminal:
	- *ftp*
 	- *open localhost*
  - provide username and password
  - *put c.txt* --> this command pushes the file into ftp
- Windows Command Prompt:
	- *ftp*
  - *open ubuntu_machine_ip_address* --> ex: *open 192.168.250.1*
  - *get c.txt* --> this command gets the file that was previously pushed from Ubuntu and places it in the Users folder
  - *!dir* --> you should see *c.txt* in the returned list
  - *put d.txt*
- Linux Terminal:
	- *get d.txt*
  - *cd ls -l* --> you should see the *d.txt* in the returned list

#### Firewall
Just as I set some firewall rules in Windows, I have done that in Linux too. I will now tell you step by step what you need to do in order to set a firewall rule, how to test it and, in the end, how to remove it. 
- open the terminal
- *sudo ufw enable* 
- *sudo ufw deny 22* --> blocks the 22 port, which is the one SSH uses
- *sudo ufw status* --> you should see port 22 as denied

That's it! Now if you open putty and try to connect to the VM, your should not be able to do so. <br/>
In case you want to use putty again, you will need to run the following commands in the Linux Terminal:
- *sudo ufw allow 22* --> allows the 22 port
- *sudo ufw disable* 


#### Server mail:


Server mail:
- switch to chatgpt
- bard@vaibhav.com

Site / virtual host:
- http://site1.com
