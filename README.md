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

<<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>1. Setting up the VM's in Azure
  
First, we create 2 azure Virtual Machines: The Domain Controller and the User. For the domain controller use Windows Server 2022 image, and for the user use Windows 10 image. Both of the VM's are put in the same virtual network named DC. The domain controller's NIC IP address is set to static 
</p>
<br />
