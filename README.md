<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/dBvSN88.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Create 2 Virtual Machines. One is called DC-1, and the other is Client-1. 
(DC is the Domain Controller) 
DC-1 is using Windows Server 2022 and C-1 is using Windows 10 Pro
<p>
</p>
<br />

<p>
<img src="https://i.imgur.com/9o7fP1h.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/oOUro5x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/PFimj2N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 with Remote Desktop and ping DC-1’s private IP, it will fail
  
Log into DC-1 and enable every ICMPv4 on the local windows Firewall

Go back to Client-1 to see the ping succeed
</p>
<br />

<p>
<img src="https://i.imgur.com/AY40NFb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/w00aVMD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/OsXd0hA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
After installing Active Directory Domain Services on DC-1, we will create a new forest (mydomain.com)

Restart DC-1 and log back in as user: mydomain.com/labuser (yourdomain/yourusername)
</p>
<br />

<p>
<img src="https://i.imgur.com/UQe1WVk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/72blYte.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/u3owy7F.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/jIj3mXz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”, and “_ADMINS”
  
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”

Add jane_admin to the “Domain Admins” Security Group

Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”

User jane_admin as your admin account from now on
</p>
<br />

<p>
<img src="https://i.imgur.com/q8BuSfJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/zbirGZo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/NFPIaed.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
  
From the Azure Portal, restart Client-1

Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)

Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

Create a new OU named “_CLIENTS” and drag Client-1 into there
</p>
<br />

<p>
<img src="https://i.imgur.com/hOwWSnM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Client-1 as mydomain.com\jane_admin and open system properties
  
Click “Remote Desktop”

Allow “domain users” access to remote desktop

You can now log into Client-1 as a normal, non-administrative user now
</p>
<br />

<p>
<img src="https://i.imgur.com/9TwDf9x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/WGzQPwU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/z2pINaG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/oq78lRI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to DC-1 as jane_admin
  
Open PowerShell_ise as an administrator

Create a new File and paste the contents of the <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1" target="_blank">script</a> into it  

Run the script and observe the accounts being created

When finished, open ADUC and observe the accounts in the appropriate OU

Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

</p>
<br />
