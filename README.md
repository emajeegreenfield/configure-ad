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

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Setup Resources in Azure</h3>
<br />
<p>
  Create the Domain Controller VM (Windows Server 2025) named “dc-1" and ensure to use the vnet you created:
</p>
<p>
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/bb5bd6fd-d545-4978-b67d-0d35e085389e" />
  <img width="1660" height="988" alt="image" src="https://github.com/user-attachments/assets/f908f65a-1556-48e9-a38c-9b7613d9f27c" />
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/9748bf13-1cf7-42df-8b30-eafb2eff61ac" />
</p>
<p>
  Create the Client VM (Windows 11) named “Client-1”. Use the same Resource Group and Vnet that was created in previous step:
</p>
<p>
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/025dac16-1418-4b8e-a625-a6d6896b588b" />
</p>
<p>
  Set Domain Controller’s NIC Private IP address to be static:
</p>
<p>
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/a7dd9480-3de5-4aca-b65f-ff6558c948ee" />
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
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/967ebc3b-b666-4546-bdaf-852ac17794c7" />
  <img width="1660" height="936" alt="image" src="https://github.com/user-attachments/assets/e41337f3-c44a-49d9-8774-54f17c50e351" />
</p>
<p>
  Login to Client-1 with the Windows app using it's public IP address:
</p>
<p>
  <img width="936" height="1068" alt="image" src="https://github.com/user-attachments/assets/419b077c-75d9-456d-9873-d8442580a725" />
</p>
Open Powershell and ping DC-1's private IP address > Run "ipconfig /all" and DNS Servers should match:
</p>
<p>
  <img width="1954" height="1018" alt="image" src="https://github.com/user-attachments/assets/2ad14f3e-e80e-4879-9d51-c7943ce0ab0e" />
  <img width="1954" height="1018" alt="image" src="https://github.com/user-attachments/assets/f5718c92-89bd-4d6a-8b1e-76d9651ba5d4" />
</p>
<h3 align="center">Install Active Directory</h3>
<br />  Login to DC-1 and install Active Directory Domain Services:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/9c2d4d99-d01f-49e6-a39b-fc58c009bfbc" />
</p>
<p>
  Promote as a Domain Controller by clicking the flag in upper right corner > Setup a new forest such as mydomain.com (can be anything, just remember what it is):
</p>
<p>
  <img width="1516" height="1018" alt="image" src="https://github.com/user-attachments/assets/438132fa-a430-486f-8c43-73a675630836" />
</p>
<p>
  Restart and then log back into DC-1 as user: mydomain.com\labuser:
</p>
<p>
  <img width="880" height="472" alt="image" src="https://github.com/user-attachments/assets/d169dc5b-fc1c-47d3-a355-834e6033ced3" />
</p>
<br />
<br />
<h3 align="center">Create an Admin and Normal User Account in AD</h3>
<br />
<p>
  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS":
</p>
<p>
  <img width="2566" height="956" alt="image" src="https://github.com/user-attachments/assets/7308cea1-73f3-45eb-a624-ca6ad1e1ec3e" />
</p>
<p>
  Create a new employee named “Jane Doe” with the username of “jane_admin”:
</p>
<p>
  <img width="1502" height="1054" alt="image" src="https://github.com/user-attachments/assets/0ed26adf-2b41-4333-bd0b-a80587fb3ff7" />
</p>
<p>
  Add jane_admin to the “Domain Admins” Security Group:
</p>
<p>
  <img width="1502" height="1054" alt="image" src="https://github.com/user-attachments/assets/37a6b92c-2139-419e-aa5b-dc02d7c6500f" />
</p>
<p>  
  Log out of DC-1 and log back in as “mydomain.com\jane_admin”:
</p>
<p>
  <img width="880" height="474" alt="image" src="https://github.com/user-attachments/assets/830ddb61-82cf-43aa-88ff-b043dbeca9f3" />
</p>
<br />
<br />
<h3 align="center">Join Client-1 to your domain </h3>
<br />
<p>
  Login to Client-1 as the original local admin (labuser) and join it to the domain:
</p>
<p>
  <img width="644" height="870" alt="image" src="https://github.com/user-attachments/assets/f0dc1797-9132-440c-9260-d77eb7e51f04" />
</p>
<p>
  Login to the Domain Controller and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.
</p>
<p>
  Create a new OU named “_CLIENTS” and drag Client-1 into there:
</p>
<p>
  <img width="1502" height="1052" alt="image" src="https://github.com/user-attachments/assets/057994e5-2596-47fc-bbd3-f6da3fb66ab9" />
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
<p>
  <img width="2044" height="1596" alt="image" src="https://github.com/user-attachments/assets/b9aafe2b-a20d-482a-ad70-eb4bd7a98c30" />
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
  Create a new File and paste the contents of this script (https://github.com/Xinloiazn/configure-ad/blob/main/adscript.ps1) into it > Run the script:
</p>
<p>
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/5b9a4d72-5ac9-4f1d-b14b-559e031be8a9" />
</p>
<p>
  When finished, open ADUC and observe the accounts in the appropriate OU and attempt to log into Client-1 with one of the accounts (take note of the password in the script):
</p>
<p>
  <img width="1502" height="1052" alt="image" src="https://github.com/user-attachments/assets/8dbacfb4-53d4-4fe1-8e30-a7362e8ad667" />
  <img width="880" height="468" alt="image" src="https://github.com/user-attachments/assets/438c4a4e-46a9-4be9-bd4b-889600ca738a" />
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/9aa25f22-9a03-4c8d-83c0-d9d1933eb367" />
</p>
<br />
<br />
<p>
  
