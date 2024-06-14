# Windows Server (WS) and Windows Client (WC)

## Making sure they connect
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


## Windows Server

### Domain
The server's domain name is domeniu.local and both the client and the server are in that domain.

### Users and groups
There are 3 users and 2 groups created:
- user1 and user2 are in group1
- user2 and user3 are in group2

### Block access to control panel (GPE)
There is a policy set on WS that blocks the access to control panel for the users. In order to see the implementation of the rules, follow these steps from Windows Server: *tools -> group policy editor -> forest -> domains -> domeniu.local*. <br/>
Once you are here, you will see 2 created rules:
- disable task manager
- no control panel
The first rule disables task manager for group1 and the second disables control panel for group2.

### File transfer
In order to change rwx (read, write, execute) permissions for a shared file within the domain, you need to follow these steps: 
- open Computer Management -> system tools -> shared folders -> shares -> propersties of sf1 -> share permissions

Now you may now change the folder's permissions. You can do so for any file you create here, which you can do by simply pressing right click on the blank space, select new share and then you can make your own configuaration for the file.


## Windows Client
### Users and groups
As iterated in the WS section, we found out that there are 3 users and 2 groups created. However, there is another user that I have not talked about yet, which is proiectso. This user was the one that was used to make the domain connection between WS and WC. I will remind you that you can find the credentials for the users in the credentials.md file. 

### Group Policy Editor
Apart from the policy set from WC for the groups, I have also set a local firewall rule in proiectso, which you will need to enable and then disable yoruself after you are done with testing it. In order to find the policy, you need to navigate to: *Group Policy Editor -> user configuration -> administrative templates -> control panel -> prohibit access to control panl -> tick enabled*. Once you have done that, the access to control panel should be prohibited. In order to disable it, simply untick the enabled box.

### Task Scheduler:
Another implemented functionality is a scheduled task. The chosen automation is opening notepad when the clock reaches a certain time. In order to test this, you will need to set the time yourself to an upcoming moment.
In order to do so, you will need to follow these steps: *open Task Scheduler -> task scheduler library -> open notepad -> properties -> triggers*. When you got here, set the time to your liking and then wait until the clock reaches that value. When that happens, notepad should open automatically.

### Script:
You may have noticed two files on the desktop already: *script.bat* and *script.txt*. Click the *script.bat* file and see what it does. <br/>
As you have probably noticed, the script created a folder on Desktop, that contains a textfile with some writing in it. 
<br/>In order to see how that was done, open *script.txt*, which contains the same script that was used to automate the folder and file creation you just saw.
