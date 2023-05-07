# Configure DNS for Active Directory
In this lab I will configure my client computer to use DC01 as its primary domain controller.

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
<img src="" alt="Microsoft DNS Logo"/>
</p>

<h1> (Azure)</h1>
This tutorial outlines the implementation of DNS within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set the client computers DNS settings to point to the domain controller DC01 from inside Azure
- Restart the client computer
- Verify communication between Domain Controller and Client Computer
- Join the client computer to the domain DC01
- Log into the domain controller, verify that the client computer appears
  in Active directory users and computers
- Setup Remote Desktop to allow all non-admin domain user access to remote desktop
- Create an OU name “Clients” and put the new client computer into that OU


<h2>Deployment and Configuration Steps</h2>

<h4>Set the client computers DNS settings to point to the domain controller DC01 from inside Azure</h4>

<p>Click on GTWS-01 the client VM  > under settings/ networking > select the network interface
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Select DNS servers > custom > enter the private IP address for DC01 “10.0.0.4”  > save
<P>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>From the Azure portal > restart GTWS-01 client to flush the old DNS settings
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4> Verify communication between Domain Controller and Client Computer</h4>

<p>Log into GTWS-01 client with RDP using the public IP address 
Use the local Admin username
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Check to see if the DNS Servers is pointing to DC01 private address 10.0.0.4

Right-click start > run > cmd

Ipconfig /all    
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Ping 10.0.0.4   to verify communication between DC01 and the client computer
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h4>Join the client computer to the domain DC01</h4>

<p>Right-click Start > system > rename this pc (advanced)
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Change > Member of Domain
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Enter the domain name > Ok
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Enter domain user name:	gterrylabdomain.com\gregory.terry
Enter password:		

This computer is now part of the domain
<p>
<img src=" " height="70%" width="70%" alt="Disk Sanitization Steps"/>



<h4>Log into the domain controller, verify that the client computer appears in Active directory users and computers</h4

<p>Restart the VM connection > log on to DC01 with RDP using the domain logon username
<p>
<img src="" height="50%" width="50%" alt="Disk Sanitization Steps"/>

</p>In Server Manager > tools > Active Directory Users and Computers >

expand the domain down to computers >

We can see that GTWS-01 is listed as a computer in the domain
</p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Setup Remote Desktop to allow all non-admin domain user access to remote desktop</h4>

<p>Log back into GTWS-01
Right-click start > system > remote desktop
<p>
<img src="" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Under User Accounts, select Users that can remotely access this PC
<p>
<img src="" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Add > domain users
<p>
<img src="" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="" height="50%" width="50%" alt="Disk Sanitization Steps"/>

</p>Go to DC01
Active Directory Users and Computers > mydomain.com > users > domain users >

Members tab	

**Here are the domain users that can access GTWS01 with RDP
</p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h4>Create an OU name “Clients” and put the new client computer into that OU</h4>

</p>Active Directory Users and Computers > right-click gterrylabdoamin.com >

new > Organizational Unit
</p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Name the OU "CLIENTS"  > OK
<p>

<p>Drag the Client Computer from the Computers OU the the Clients OU
<p>

</p>In the next lab I will create new users with a PowerShell script and attempt

to log on to the domain controller with one of the new users.
</p>
