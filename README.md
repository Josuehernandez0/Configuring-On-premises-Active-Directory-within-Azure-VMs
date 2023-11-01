# Configuring-On-premises-Active-Directory-within-Azure-VMs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<p align="center">
<img src="https://i.imgur.com/N2J81cC.png"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group
- Create Virtual Machine Windows Server Datacenter
- Create Virtual Machine Windows 
- Use Remote Dektop Connection to log into Cilent-1 VM
- Grab the Private IP of DC-1 to do a endless ping on Cilent-1 VM in Command Prompt
- Go to DC-1 to load wf.msc to allow the ping to occur in inbound rules
- Go to Server Manager to add roles and features
- Create a Active Directory Domain Services
- Promote the server to a domain controller and create a new forest
- Log back into DC-1 VM by using mydomian.com\labuser
- In DC-1 go to tools, and go to Active Directory Users and Computers
- Create a new organizational unit folder called _EMPLOYEES
- Create another new organizational unit folder called _ADMINS
- Create new user in ADMINS folder
- Put new user in Domain Admins then logoff of DC-1
- Log back into DC-1 under Admin account
- Go back to Cilent-1 and rename this pc under a new domain, but will recieve an error
- Copy DC-1 Privite NIC IP then paste in Cilent-1 DNS Servers
- Restart Cilent-1 VM
- Log into Cilent-1 VM using Remote Desktop Connection
- Rename this PC again in Cilent-1 VM
- Change the Domain name to user Admins
- Restart VM again
- Log into Cilent-1 VM under admin account using Remote Desktop Connection
- Use Remote Desktop to let Domain Users log into the account
- Go back to DC-1 VM and go to the Users folder to see both labuser and admin account in Domain Users
- Run Windows Powershell ISE as administrator
- Create a new file and run script for creating 2000 users
- Go to _EMPLOYEES folder and grab one's display name
- Logoff of Cilent-1 VM then log back into Cilent-1 VM under user you picked
- Logoff Cilent-1 as random user
- Grab another random user Display name
- Log back into Cilent-1 VM with new user but mistype password to get kicked out of account
- Go to DC-1 VM and manually reset the password or unlock the account

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/w1psRtI.png"/>
</p>
<p>
First go to Microsoft Azure and type Resource Group 
</p>
<br />

<p>
<img src="https://i.imgur.com/qUbDlfz.png"/>
</p>
<p>
Next click create to create the Resource Group
</p>
<br />

<p>
<img src="https://i.imgur.com/ZY1wIfO.png"/>
</p>
<p>
Now for the name type AD-LAb and the region under US West US 3 then go to the review and create tab 
</p>
<br />


<p>
<img src="https://i.imgur.com/DWS0odj.png"/>
</p>
<p>
Next the validation pass through 
</p>
<br />


<p>
<img src="https://i.imgur.com/bXEBGJA.png"/>
</p>
<p>
Now once the process is done you will see the Resource Group was created 
</p>
<br />

<p>
<img src="https://i.imgur.com/XEhQFAg.png"/>
</p>
<p>
Type Virtual Machine in the search bar 
</p>
<br />

<p>
<img src="https://i.imgur.com/vxN4oR1.png"/>
</p>
<p>
Next click Azure Virtual Machine to create the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/awqKr81.png"/>
</p>
<p>
Now for the resource group click AD-LAb, and the virtual machine name type DC-1. The region put under US West US 3 and the image under Windows Server
</p>
<br />

<p>
<img src="https://i.imgur.com/OOkC9dp.png"/>
</p>
<p>
Next the size needs to be under Standard E2 and teh username under labuser and the password under your own unique password. Remember to open a notepad and type all your info out so you dont lose it.
</p>
<br />

<p>
<img src="https://i.imgur.com/uHq2zjd.png"/>
</p>
<p>
Next click the box in the Licensing section and then click th econfirm box. Then click review and create 
</p>
<br />

<p>
<img src="https://i.imgur.com/tfSIhRn.png"/>
</p>
<p>
Now go to the networking tab and make sure the virtual network, subnet, and the public IP all says (new)
</p>
<br />

<p>
<img src="https://i.imgur.com/EmHpCfI.png"/>
</p>
<p>
Now go to the review and create section 
</p>
<br />

<p>
<img src="https://i.imgur.com/CvW4woT.png"/>
</p>
<p>
Next let the deployment progess load 
</p>
<br />

<p>
<img src="https://i.imgur.com/jcExvfg.png"/>
</p>
<p>
Now the process will be complete when there is a green check 
</p>
<br />

<p>
<img src="https://i.imgur.com/rPMnpd5.png"/>
</p>
<p>
Next type virtual machine and you will see DC-1 VM was created
</p>
<br />

<p>
<img src="https://i.imgur.com/Y9F6T6d.png"/>
</p>
<p>
Next click create and then go to Azure Virtual Machine 
</p>
<br />

<p>
<img src="https://i.imgur.com/Kjvftpd.png"/>
</p>
<p>
Next in the subscriiption section make sure the same subscription that you used for the resource group is selected. Then in Resource Group click AD-Lab then for the name type Cilent-1 and the region click US West US 3
</p>
<br />

<p>
<img src="https://i.imgur.com/7uNy1ZV.png"/>
</p>
<p>
Now for the Image click Windows 10 pro version and the size click Standard E2
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next for the username type labuser and the password the same as DC-1 VM. Then click the Licensing tab then click review and create 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now the deployment will be done when a green check appears next to the deployment
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type virtual machines in the search bar 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next you will see that DC-1 and Cilent-1 was created 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now click DC-1 and click networkng 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click on the Network Interface 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click on IP Configurations 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now click ipconfig1
</p>
<br />

<p>
<img src=""/>
</p>
<p>
We are editing the IP Configurations in the allocation section click Static instead of Dynamic then click save.
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now we are going to log into Cilent-1 VM copy the public IP address
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type Remote Desktop Connection and click to open the app
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next paste the IP of Cilent-1 in the computer section 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
<img src=""/>
</p>
<p>
Now tpye for the username type labuser and the password type the password you made for the VM, then click ok
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click yes to open the VM
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now you should see the VM loading under the name labuser 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click no to the following image above 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Once networks load click yes 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now open up command prompt 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next go back to Azure and copy the Private IP of DC-1
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Go back to Cilent-1 VM and type ping -t the the private IP of DC-1. We are doing a endless ping to see the traffic 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Then go to Azure and grab the Public IP of DC-1 VM then load Remote Desktop Connection and open the app  
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Paste the IP of DC-1 in the computer section then click connect 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type the username labuser and the password you made for DC-1 VM then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click yes to log into the VM
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Once the VM loads let Server Manager load as well. Next once networks load click yes 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type wf.msc in the search bar of DC-1 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click on Inbound Rules 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click the protocol, then look for ICMPv4 protcol
</p>
<br />


<p>
<img src=""/>
</p>
<p>
Next right click then enable rule for the following in the image above 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Go back to Cilent-1 VM and you wil see the constant pinging click Ctrl + C then go back to the directory
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next go to DC-1 and click add roles and features 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click the box for Active Directory Domain Services 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click the add features 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click Install 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next let the installation process start
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Once the process finishes click close 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click the caution symbol near manage on the top right 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click Promote this server to a domain controller 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Click add a new forest then type mydomain.com then click next. {NOTE} you can type anything you want just have a .com at the end of it please copy it down to your notepad to not forget 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type the password in for this my password will be Password1 then click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click next
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click install to finish creating the domain controller 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Then let the installation process finish 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
You might see the image above for Reconnecting dont click cancel let the VM bandwidth connect back only if it doesnt kick you out properly then click cancel 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Go back to Azure and click DC-1 copy the public IP 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type Remote Desktop Conenction and open the app 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now since we made DC-1 under another name click more choices then click use a different account 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next tpye in mydomain.com\labuser for the username and the password is Password1 then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click yes to log into the VM {NOTE} if it doesnt work the first time try again to log in. If it still doesn't let you then close Remote Desktop Connection and do the process again 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now once you are in the DC-1 VM let Server Manager load on the screen 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click Tools on the top right then go to Active Directory Users and Computers 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click on mydomain.com folder on the left side 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next right click anywhere and go to new then to organizational unit 
</p>
<br />


<p>
<img src=""/>
</p>
<p>
Next type _EMPLOYEES then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now go back to mydomain.com and right click anywhere again, go to new then to organizational unit 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type ADMINS then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
In ADMINS right click then go to new then to user
</p>
<br />

<p>
<img src=""/>
</p
<p>
For the first name type jane and the intials can be doe or the last name can be doe. For the user logon name type jane_admin then click next 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next for the password type Password1 then uncheck user must change password at next login  
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next check the box for Password never expires then click next
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Then finish to create the user 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now you should see jane doe account in the ADMINS folder if not right click then go to refresh 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next right click the account and go to properties 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next the member of tab then click add 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next in the enter section type domain then click check names 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next double click on Domain Admins then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Then click apply to finish 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next open command prompt then type whoami you will see we are still under labuser and not jane doe next type logoff 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Go back to Azure and click DC-1 and copy the Public IP
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next paste DC-1 VM public IP then click connect 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click more choices then click use a different account
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next type mydomain.com\jane_admin in the username then the password is still Passsword1 then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click yes to log into DC-1 VM
</p>
<br />

<p>
<img src=""/>
</p>
<p>
DC-1 VM should load and you will see the name jane doe.
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Open command line then type whoami and you will see you are logged in as jane_admin 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next right click the windows icon on the bottom left then click the system file 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now click Rename this PC (advanced)
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click change 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
<img src=""/>
</p>
<p>
Next click member of and click the domain circle, then type domain.com then click ok 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now you will see an error displyed on the screen click ok this is because we have to change the NIC in azure for Cilent-1
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Now go to the Azure portal and go to Virtual Machine then click DC-1, copy the NIC Private IP
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click Cilent-1 and go to Network Interface and click on cilent 
</p>
<br />

<p>
<img src=""/>
</p>
<p>
Next click DNS servers then click custom 
</p>
<br />

<p>
<img src="https://i.imgur.com/qdASf5z.png"/>
</p>
<p>
Now paste the NIC Private IP of DC-1 then click save 
</p>
<br />

<p>
<img src="https://i.imgur.com/MPzv9qi.png"/>
</p>
<p>
Next let the process change the NIC
</p>
<br />

<p>
<img src="https://i.imgur.com/l2UiPPO.png"/>
</p>
<p>
Once its done you will see a green check you can click the bell icon to see the prcess load 
</p>
<br />

<p>
<img src="https://i.imgur.com/ZE2DOep.png"/>
</p>
<p>
Next go back to Virtual Machine adn click restart then click yes to restart Cilent-1 VM
</p>
<br />

<p>
<img src="https://i.imgur.com/lMRPjRF.png"/>
</p>
<p>
You can click the bell icon and see the process restart the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/Jx9gflo.png"/>
</p>
<p>
Once its done you will see a green check mark icon 
</p>
<br />

<p>
<img src="https://i.imgur.com/MQ1rKbV.png"/>
</p>
<p>
Next click Cilent-1 then copy the public IP 
</p>
<br />

<p>
<img src="https://i.imgur.com/qYS9lXP.png"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://i.imgur.com/VN8NdDw.png"/>
</p>
<p>
Next paste the Public IP in the computer section and then click connect 
</p>
<br />

<p>
<img src="https://i.imgur.com/Bu8q1Ki.png"/>
</p>
<p>
Now type labuser for the username and the original password you made for Cilent-1 then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/T1KrIsp.png"/>
</p>
<p>
Next press yes to log into the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/tqNbFR9.png"/>
</p>
<p>
Now you will see Cilent-1 VM load under labuser 
</p>
<br />

<p>
<img src="https://i.imgur.com/Adub5cJ.png"/>
</p>
<p>
We are going to do the same process as before right click the windows icon then click on system 
</p>
<br />

<p>
<img src="https://i.imgur.com/ve23aPw.png"/>
</p>
<p>
Next click Rename this PC (advanced)
</p>
<br />

<p>
<img src="https://i.imgur.com/Zt4ak7C.png"/>
</p>
<p>
Now click change 
</p>
<br />

<p>
<img src="https://i.imgur.com/g8YHRup.png"/>
</p>
<p>
Now click domain and type mydomain.com then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/SfTLzOF.png"/>
</p>
<p>
Now Computer Name / Domain Changes should load on your screen 
</p>
<br />

<p>
<img src="https://i.imgur.com/gxv1vGI.png"/>
</p>
<p>
Next type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/aQRU7kp.png"/>
</p>
<p>
You will see the VM is trying to reconnect dont click cancel let the bandwidth conenct back to the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/tXVcdpb.png"/>
</p>
<p>
Next you will see a Please wait page 
</p>
<br />

<p>
<img src="https://i.imgur.com/ihd3Q83.png"/>
</p>
<p>
Close out of everything, but you wil see a tab that says You must restart your computer to apply these changes then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/TH8zYWX.png"/>
</p>
<p>
Then click Restart Now to restart the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/gOYO1Gb.png"/>
</p>
<p>
Next you will see a Restarting Screen load 
</p>
<br />

<p>
<img src="https://i.imgur.com/IPuQzDX.png"/>
</p>
<p>
It will kick you out of Cilent-1 VM now go back to get the Public IP then type Remote Desktop Connection and open the app 
</p>
<br />

<p>
<img src="https://i.imgur.com/aHU0gkH.png"/>
</p>
<p>
Next paste the public IP in the computer section then click connect 
</p>
<br />

<p>
<img src="https://i.imgur.com/kMNYu2H.png"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://i.imgur.com/cavQ1cV.png"/>
</p>
<p>
Now type mydomain.com\jane_admin then the password is Password1 then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/eukZtNR.png"/>
</p>
<p>
Next click yes to connect to the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/IxAiJrD.png"/>
</p>
<p>
Now you will see the Cilent-1 VM loading as jane doe 
</p>
<br />

<p>
<img src="https://i.imgur.com/i8ovTcp.png"/>
</p>
<p>
Next right click the windows icon then click system 
</p>
<br />

<p>
<img src="https://i.imgur.com/yZ5L9YZ.png"/>
</p>
<p>
Next click Remote Desktop 
</p>
<br />

<p>
<img src="https://i.imgur.com/pimuzeR.png"/>
</p>
<p>
Now click Select users that can remotely access this PC
</p>
<br />

<p>
<img src="https://i.imgur.com/TQbctCk.png"/>
</p>
<p>
Next click add 
</p>
<br />

<p>
<img src="https://i.imgur.com/3SW3zsT.png"/>
</p>
<p>
Type domain users then click check names 
</p>
<br />

<p>
<img src="https://i.imgur.com/z3HzGNH.png"/>
</p>
<p>
You will see the name changed to CAPS with a underscore then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/eGdedSr.png"/>
</p>
<p>
Next click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/XnHXgKq.png"/>
</p>
<p>
Go back to DC-1, another way to get to Users and Computers is to click the windows icon on the bottom left. Next click Windows Administrative Tools then click Active Directory Users and Computers
</p>
<br />

<p>
<img src="https://i.imgur.com/lIOsgfI.png"/>
</p>
<p>
Next click users then click Domain Users
</p>
<br />

<p>
<img src="https://i.imgur.com/tnULLj6.png"/>
</p>
<p>
Now you will see jane doe and labuser are under the Domain Users
</p>
<br />

<p>
<img src="https://i.imgur.com/liIx60G.png"/>
</p>
<p>
Next type Windows Powershell ISE right click and run as administrator
</p>
<br />

<p>
<img src="https://i.imgur.com/GJEq0od.png"/>
</p>
<p>
Now click yes to run the software 
</p>
<br />

<p>
<img src="https://i.imgur.com/pa5fawi.png"/>
</p>
<p>
Click file then click new 
</p>
<br />

<p>
<img src="https://i.imgur.com/aqoToVC.png"/>
</p>
<p>
Go to the Link and copy the code this code will create 2000 users https://github.com/josuehernandez0/Generate-Names-Create-Users.ps1/blob/main/README.md
</p>
<br />

<p>
<img src="https://i.imgur.com/PSq00E3.png"/>
</p>
<p>
Now paste the code in the white blank page section 
</p>
<br />

<p>
<img src="https://i.imgur.com/YaAxLwF.png"/>
</p>
<p>
Now click the green play icon to run the script 
</p>
<br />

<p>
<img src="https://i.imgur.com/JVX7zHJ.png"/>
</p>
<p>
Now in the blue section you will see the 2000 users being created in a ligth blue color 
</p>
<br />

<p>
<img src="https://i.imgur.com/UHZnpmD.png"/>
</p>
<p>
Next click on the _EMPLOYEES folder then right click and click refresh 
</p>
<br />

<p>
<img src="https://i.imgur.com/IhDFjXI.png"/>
</p>
<p>
Now you will see the current users that have been created 
</p>
<br />

<p>
<img src="https://i.imgur.com/86DWrtm.png"/>
</p>
<p>
Next go to Cilent-1 open up the command line then type logoff, then press enter 
</p>
<br />

<p>
<img src="https://i.imgur.com/KUEAdgU.png"/>
</p>
<p>
Now that we logged out of Cilent-1 we are going to go to DC-1 VM and pick a user then copy the display name. 
</p>
<br />

<p>
<img src="https://i.imgur.com/bhtgtyN.png"/>
</p>
<p>
Open up your notepad and paste or type the display name of the account you want to log into  
</p>
<br />

<p>
<img src="https://i.imgur.com/daqolD2.png"/>
</p>
<p>
Now type Remote Desktop Connection and open the app
</p>
<br />

<p>
<img src="https://i.imgur.com/v3UPIFf.png"/>
</p>
<p>
Next paste the public IP of Cilent-1 VM then click connect
</p>
<br />

<p>
<img src="https://i.imgur.com/kn0G4d7.png"/>
</p>
<p>
Next click more choices and click use a different account 
</p>
<br />

<p>
<img src="https://i.imgur.com/RXiFqGd.png"/>
</p>
<p>
Now type mydomain.com\ then your username. Next for the password type Password1 refer to the image above then press ok
</p>
<br />

<p>
<img src="https://i.imgur.com/FVXdIxN.png"/>
</p>
<p>
Next press yes to connect to the VM
</p>
<br />

<p>
<img src="https://i.imgur.com/yBGj5br.png"/>
</p>
<p>
Now you will see the username display on the screen of the loading screen of Cilent-1 VM
</p>
<br />

<p>
<img src="https://i.imgur.com/s8SxQm2.png"/>
</p>
<p>
Open commandline and type whoami and you will see we are logged in as the user you picked. Type hostname and you will see you are still under Cilent-1 then type logoff 
</p>
<br />

<p>
<img src="https://i.imgur.com/Q4pWgDO.png"/>
</p>
<p>
Go back to DC-1 VM and pick another user, then copy the display name 
</p>
<br />

<p>
<img src="https://i.imgur.com/4dnsfRo.png"/>
</p>
<p>
Type Remote Desktop Connection and load the app 
</p>
<br />

<p>
<img src="https://i.imgur.com/DemCRmP.png"/>
</p>
<p>
Next paste the Public IP of Cilent-1 then click connect 
</p>
<br />

<p>
<img src="https://i.imgur.com/BU9a5ta.png"/>
</p>
<p>
Click more choices then click use a different account 
</p>
<br />

<p>
<img src="https://i.imgur.com/7sn1fm6.png"/>
</p>
<p>
Now type mydomain.com\ then the username, but for the password type the password incorrectly ten times to lock you out of your account refer to the image above 
</p>
<br />

<p>
<img src="https://i.imgur.com/8wHv8rN.png"/>
</p>
<p>
<img src="https://i.imgur.com/Cak8YWi.png"/>
</p>
<p>
Next go back to DC-1 VM and go to the account tab of the user you picked. Click th box Unlock account then click ok 
</p>
<br />

<p>
<img src="https://i.imgur.com/LJSF4MV.png"/>
</p>
<p>
You can also right click the user you picked and click reset password, or even disable the account 
</p>
<br />

<p>
<img src="https://i.imgur.com/lMRNqnV.png"/>
</p>
<p>
Now to see Lab 6 https://github.com/josuehernandez0/Create-Inspect-and-Delete-DNS-A-Records-and-CNAME and Lab 7 https://github.com/josuehernandez0/Network-File-Shares-and-Permissions 
</p>
<br />
