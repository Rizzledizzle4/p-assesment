<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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

- Create Resources in Azure
 
- Install Active Directory
- Join Client-1 to the Domain
  

<h2>Deployment and Configuration Steps</h2>


![image](https://github.com/Rizzledizzle4/p-assesment/assets/135624545/9172f11a-b641-4820-a79e-58369465131e)

Create a Resource Group.

Create a virtual machine within Azure with Windows 2022 as the Operating Systems.Make sure to select the resource group you created.Name this VM DC-1.Set the Domain Controller's NIC Private IP address to static.

Create another virtual machine with windows 10 as the Operating System.Name this Client 1.Use the same resource group.

Confirm connectivity between Client1 and DC-1 by logging into client 1 and pingin dc-1's private IP adresss.After this fails login into DC-1 open Windows Firewall Settings and enable ICMPv4.

Log into Client1 again and ping DC-1's Private IP to verify a successful connection.


![image](https://github.com/Rizzledizzle4/p-assesment/assets/135624545/ad9c9436-08b4-4c5e-914e-cd9e6c4b23d9)


Log into DC-1 and open Server Manager.

Within Server Manager click on "add roles and features"and select Active Directory Domain Services and install.

Once installed click on the caution sign to promote DC-1 to a Domain Controller.Setup a new forest with the domain name "mydomain.com."Restart DC-1
and login as user mydomain.com\labuser.

Within Active Directory create 2 Organizational Units(_EMPLOYEES,_ADMINS)

Within the OU (_ADMINS)create the user Jane Doe with the username jane_admin.Add jane_admin to the "Domain Admins"security group.

Log out of DC-1 and log back in using username "mydomain.com\jane_admin"from now on.


![image](https://github.com/Rizzledizzle4/p-assesment/assets/135624545/4b82d03e-e8af-476e-af39-0fcec3bf7bdd)


In Azure set Client1's DNS settings to the DC-1's Private IP address. Restart Client1 from the Azure Portal.

Log in to Client-1 using Remote Desktop as the original local admin ("labuser"). Join Client1 to the domain and wait for the computer to restart. 

Log in to the Domain Controller using Remote Desktop and verify that Client1 appears in ADUC inside the "Computers" container in the root of the domain.


