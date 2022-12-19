<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup the VM's in Azure
- Install Active Directory
- Create Admin/User Accounts in AD
- Configure AD for Admin/Users 

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>1. Setting up the VM's in Azure</h2>
  
First, we create 2 azure Virtual Machines: The Domain Controller and the User. For the domain controller use Windows Server 2022 image, and for the user use Windows 10 image. Both of the VM's are put in the same virtual network named DC. The domain controller's NIC IP address is set to static 
</p>
<br />

<p> 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>2. Ensuring Connectivity between the Client and Domain Controller</h2>

To check connectivity simply ping the DC's private IP. By default, Windows Server has echo requests from ICMPv4 blocked in the firewall, meaning the pings are going to drop. To change this we use RDP to open the DC's VM and change these settings in the windows firewall. Now when we ping the DC's private IP we see responses ensuring our connect is good. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>3. Installing Active Directory on the DC</h2>

Open server manager on the DC (comes default on Windows Server). Head to add roles and features too add Windows Domain Controller. From here we head to the 
flag in the top right to continue configuring the domain. The domain I set is testdomain.com, this is private so it can be set to anything. After going through the installation process the VM must be restarted. Now that it is a domain controller, we must login with the context of the domain (FQD). 
