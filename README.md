# Vitual Private Network (VPN)
<p align="center">
<img src="https://i.imgur.com/MntON5Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h1>VPN - Prerequisites and Installation</h1>
This tutorial covers the prerequisites and installation process for setting up and using a VPN..<br />

<h2>Environments and Technologies Used</h2>

- A VPN (Proton VPN)
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/WKnl1Gd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Resource Group in Azure, then deploy a Windows 10 Virtual Machine within it. Once the VM is set up, use Remote Desktop Protocol (RDP) to log into the VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/qUT7bSY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once inside the VM, open a web browser and navigate to https://whatismyipaddress.com/. View the IP information displayed and record it in Notepad or on a piece of paper for later reference.
</p>
<br />

<p>
<img src="https://i.imgur.com/fUjDc38.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/o4XhJYA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On your personal computer, sign up for the free version of Proton VPN at https://account.protonvpn.com/signup?plan=free&language=en.
Inside the VM, download and install the Proton VPN client. Log in to the client using your Proton VPN credentials at 
https://account.protonvpn.com/login 
</p>
<br />

<p>
<img src="https://i.imgur.com/dLrsRDw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign in to the Proton VPN client using the credentials you created during account setup. Once logged in, click "Quick Connect" to automatically connect to a VPN server. Connecting to the VPN will mask your real IP address and encrypt your internet traffic, enhancing privacy and security.
</p>
<br />

<p>
<img src="https://i.imgur.com/I1ozIdQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Revisit https://whatismyipaddress.com/ and observe the changes in the IP information. Note how the IP now reflects the VPN server you connected to, demonstrating the VPN's effect.
</p>
<br />
