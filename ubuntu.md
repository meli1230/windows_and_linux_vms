## Ubuntu
### Making the machine run properly
Before jumping into the functionalities that I have implemented, you need to make a few changes in a file, in order to make sure that the IP address used in it is the same as the one of the VM. What you need to modify is located in etc/hosts, which you can reach by typing the follow these steps: 
- open Terminal and type *ipconfig*- in the returned result, search for inet, which should be followed by your ip address
- the next command we need to type in the terminal is *sudo nano /etc/hosts*
Once you opened this file, you need to replace every ip address you see with your ip address, which you have just discovered by using *ifconfig*. When done, press *ctrl+x* to save the file and then enter to exit.

### SSH Putty
The first thing that I installed on my virtual machine is SSH, which stands for Secure Shell. This a protocol that will let use an app like putty to remotely connect to our virtual machine from any other machine, regardless of the native operating system. To test putty you need to first install the app on your physical machine or on any other machine you would like. You can use [this link](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) to simply get an exe file, from the *Alternative binary file* section.<br/><br/>
Once it downloaded, open *putty.exe*. In the window that just opened, make sure that *Port 22* is selected, as well as *Connection type: SSH* and, after that, write the IP address of the Ubuntu VM in the *Host Name (or IP address) section*. If you have done that correctly, a terminal-like window should pop up, requesting a username and password. <br/><br/>
Use the credentials provided in the *credentials.md* file and be weary of the fact that whenever you type the password, characters are being written down without anything being shown on screen, so you are typing, even if you don't have any feedback to confirm that.<br/>
You may now continue to use putty in the same way you would use the Terminal on the VM.

### Users
In order to switch between users in the terminal, use the command *su user_name*. For example, to switch to user1 we would write *su user1*.

### VSFTPD
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

### Firewall
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
Another available functionality from the Terminal is sending an email. For that, I have used Postfix Dovecott and I have only implemented the email sending. To test this service, run in the Terminal:
- *su chatgpt* --> switching to *chatgpt* user
- *mutt* --> access the mail service
- if prompted, press *a*
- press *m* to start the process of sending a new email

At the bottom of the window, yoy should be prompted to write the recipient of your email, which is where you will write *bard@vaibhav.com*, in order to send an email to the *bard* user. After that, you will need to fill in a subject and, in the end, an editable file will open. This is where the body of the email is. Once you typed anything there, you may save by pressing *ctrl+x*. In the end, press *y* to send.

#### 


Site / virtual host:
- http://site1.com
