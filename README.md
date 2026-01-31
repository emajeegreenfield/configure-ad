<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="40%" width="70%"alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />





<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Windows App (MacOS)
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2025
- Windows 11

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Setup Resources in Azure</h3>
<br />
<p>
  Create the Domain Controller VM (Windows Server 2022) named “dc-1" and ensure to use the vnet you created:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/01dfd6e4-84f2-47d2-9368-1ec554d88720" />
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/77b71f82-acc9-43f4-838b-007727859646" />
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/fc21e88d-3efd-4a7c-9d7c-43a59f1f9523" />
</p>
<p>
  Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/49135889-3ae3-446b-b243-d5d1da14572d" />
</p>
<p>
  Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/593b5f94-a02f-4f49-b38c-c39070120489" />
</p>
<p>
  
<p>
<br />
<br />
<h3 align="center">Ensure Connectivity between the client and Domain Controller</h3>
<br />
<p>
  Login to dc-1 with the Windows app using it's public IP address:
</p>
<p>
  <img width="936" height="1068" alt="image" src="https://github.com/user-attachments/assets/c63724c3-eef3-473c-83c4-8c35415d2fca" />
</p>
<p> Right click Start menu and run "wf.msc" > Click Windows Defender Firewall Properties > Turn off all firewall settings:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/c63fb34b-17be-46ac-9a21-da2bc9038af1" />
</p>
<p>
  Set Client-1's DNS settings to DC-1's private IP address and restart Client-1:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/cdfe74b6-f826-47f7-a740-a81af8d473f6" />
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/2c6ce208-6a7b-414b-b590-f1a3a562c01b" />
</p>
<br />
<br />
<h3 align="center">Install Active Directory</h3>
<br />
<p>
  Login to Client-1 with the Windows app using it's public IP address:
</p>
<p>
  <img width="936" height="1068" alt="image" src="https://github.com/user-attachments/assets/419b077c-75d9-456d-9873-d8442580a725" />
</p>
  Login to DC-1 and install Active Directory Domain Services:
</p>
<p>
  <img src="https://i.imgur.com/A1V9XJ5.png" height="75%" width="100%" alt="active directory install"/>
</p>
<p>
  Promote as a Domain Controller:
</p>
<p>
  <img src="https://i.imgur.com/zi15fw4.png" height="75%" width="100%" alt="domain controller promotion"/>
</p>
<p>
  Setup a new forest as myactivedirectory.com (can be anything, just remember what it is - I ultimately did set it up as myadproject.com which you'll see in the next pic):
</p>
<p>
  <img src="https://i.imgur.com/DCFUVrM.png" height="75%" width="100%" alt="set new forest"/>
</p>
<p>
  Restart and then log back into DC-1 as user: myadproject.com\labuser:
</p>
<p>
  <img src="https://i.imgur.com/7UakWMQ.png" height="75%" width="100%" alt="fqdn login"/>
</p>
<br />
<br />
<h3 align="center">Create an Admin and Normal User Account in AD</h3>
<br />
<p>
  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS":
</p>
<p>
  <img src="https://i.imgur.com/cYmv0r7.png" height="75%" width="100%" alt="organizational unit"/>
  <img src="https://i.imgur.com/v02CBPI.png" height="75%" width="100%" alt="organizational unit"/>
</p>
<p>
  Create a new employee named “Jane Doe” with the username of “jane_admin”:
</p>
<p>
  <img src="https://i.imgur.com/h546E6L.png" height="75%" width="100%" alt="admin creation"/>
</p>
<p>
  Add jane_admin to the “Domain Admins” Security Group:
</p>
<p>
  <img src="https://i.imgur.com/mnLwTgq.png" height="75%" width="100%" alt="security group"/>
</p>
<p>  
  Log out/close the Remote Desktop connection to DC-1 and log back in as “myadproject.com\jane_admin”. Use jane_admin as your admin account from now on:
</p>
<p>
  <img src="https://i.imgur.com/xWZ4Kol.png" height="75%" width="100%" alt="admin login"/>
</p>
<br />
<br />
<h3 align="center">Join Client-1 to your domain (myadproject.com)</h3>
<br />
<p>
  From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address:
</p>
<p>
  <img src="https://i.imgur.com/1KRsjI6.png" height="75%" width="100%" alt="client dns settings"/>
</p>
<p>
  From the Azure Portal, restart Client-1.
</p>
<p>
  Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart):
</p>
<p>
  <img src="https://i.imgur.com/50wszcP.png" height="75%" width="100%" alt="domain joining"/>
</p>
<p>
  Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.
</p>
<p>
  Create a new OU named “_CLIENTS” and drag Client-1 into there:
</p>
<p>
  <img src="https://i.imgur.com/vB1n9m0.png" height="75%" width="100%" alt="active directory client verification"/>
</p>
<br />
<br />
<h3 align="center">Setup Remote Desktop for non-administrative users on Client-1</h3>
<br />
<p>
  Log into Client-1 as mydomain.com\jane_admin and open system properties.
</p>
<p>
  Click “Remote Desktop”.
</p>
<p>
  Allow “domain users” access to remote desktop.
</p>
<p>
  You can now log into Client-1 as a normal, non-administrative user now.
</p>
<p>
  Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab):
</p>
<p>
  <img src="https://i.imgur.com/8BfpT3s.png" height="75%" width="100%" alt="remote desktop setup"/>
</p>
<br />
<br />
<h3 align="center">Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>
<br />
<p>
  Login to DC-1 as jane_admin
</p>
<p>
  Open PowerShell_ise as an administrator.
</p> 
<p>  
  Create a new File and paste the contents of this script (https://github.com/Xinloiazn/configure-ad/blob/main/adscript.ps1) into it:
</p>
<p>
  <img src="https://i.imgur.com/0i8uApf.png" height="75%" width="100%" alt="create users script"/>
</p>
<p>
  Run the script and observe the accounts being created:
</p>
<p>
  <img src="https://i.imgur.com/6QOGzs6.png" height="75%" width="100%" alt="observe create users script"/>
</p>
<p>
  When finished, open ADUC and observe the accounts in the appropriate OU and attempt to log into Client-1 with one of the accounts (take note of the password in the script):
</p>
<p>
  <img src="https://i.imgur.com/ZZCfiCp.png" height="75%" width="100%" alt="employee user accounts"/>
  <img src="https://i.imgur.com/7gBpNzN.png" height="75%" width="100%" alt="employee user selection"/>
  <img src="https://i.imgur.com/cqsddjn.png" height="75%" width="100%" alt="employee user login"/>
</p>
<br />
<br />
<p>
  I hope this tutorial helped you learn a little bit about network security protocols and observe traffic between virtual machines. This can be easily done on a PC or a Mac. Mac would just have an extra step to download the Remote Desktop App.
</p>
<p>
  Now that we're done, DON'T FORGET TO CLEAN UP YOUR AZURE ENVIRONMENT so that you don't incur unnecessary charges.
</p>
<p>
  Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion.
</p>
