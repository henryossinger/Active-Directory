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
<img src="https://imgur.com/xf441SI.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/N7nOA2Y.png" height="90%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>1. Setting up the VM's in Azure</h2>
  
First, we create 2 Azure Virtual Machines: The Domain Controller and the User. For the domain controller use Windows Server 2022 image, and for the user use Windows 10 image. Both of the VM's are put in the same virtual network named AD. The domain controller's private IP address is set to static 
</p>
<br />

<p> 
<img src="https://imgur.com/zC3PyH9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>2. Ensuring Connectivity between the Client and Domain Controller</h2>

To check connectivity simply ping the DC's private IP. By default, Windows Server has echo requests from ICMPv4 blocked in the firewall, meaning the pings are going to drop. To change this we use RDP to open the DC's VM and change these settings in the windows firewall. Now when we ping the DC's private IP we see responses ensuring our connection is good. 
</p>
<br />

<p>
<img src="https://imgur.com/fxh3rR0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>3. Installing Active Directory on the DC</h2>

Open server manager on the DC (comes default on Windows Server). Head to add roles and features too add Windows Domain Controller. From here we head to the 
flag in the top right to continue configuring the domain. The domain I set is testdomain.com, this is private so it can be set to anything. After going through the installation process the VM must be restarted. Now that it is a domain controller, we must login with the context of the domain (FQDN). 
</p>
<br />

<p>
<img src="https://imgur.com/eQI4gd9.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>  
</p>
<p>
<h2>4. Creating Admins and Users in Active Directory</h2>

Open Active Directory Users and Computers through the tools tab in the top right of the server manager. We can now create some users and admins for our domain. To create a group, right click and in the drop down select add an organizational unit. The first one will be Admins and the second one will be Employees. Once created head to the admin folder, right click, and select add user. We will create a dummy admin user and name him John Doe. Under his properties, go to the members of tab and put him in the admin group. Our John Doe is now an admin of our domain with the ability to create user accounts and more. We are also able to login using John Doe's credentials.
</p>
<br />

<p>
<img src="https://imgur.com/eQI4gd9.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/N7nOA2Y.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>5. Joining our User PC to the domain</h2>

First we must set the User PC's DNS settings to the DC's private IP. We do this in the VM's VNIC on Azure. We must configure the DC as our DNS because the domain we are using is not a public domain, only the DC knows of its existence. Once done login and edit the system domain to testdomain.com and sign in with our John Doe admin account. After completion we must restart the VM. Our user PC is now succesfully a member of the domain. Going back into Active Directory we can see all of the user accounts we currently have. (John is not in here because he is in the admin group. If he is added to the users group he will be in here) 

We now are able to create employee and admin accounts, all with the ability to login to the same User PC. Similar to a situation at school or work where multiple people are able to sign into the same PC. 

Extremely basic rundown of how Active Directory and DC's operate, none the less a fun experience. 

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>6. Using a Python script to add users</h2>

As an example, we can use a python script to create users in our DC. This script from github creates user accounts and inputs them into our DC. For testing purposes I tell it to create 10,000 users and set the password to "Password1" on all of them. The usernames are generated randomly in an algorithm within the script. 

We can choose anyone of the created users and input their credentials to login to the User PC. 
</p>
<br />
