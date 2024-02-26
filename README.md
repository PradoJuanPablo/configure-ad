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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD

<h2>Setup Resources in Azure</h2>

<p>
<img width="773" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/7ac1cd41-c488-4053-acbf-ebb1954a4cc0">

<img width="767" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/80902734-974e-4c5d-ad05-215f13e9f380">


</p>
<p>
First, we create our VMs. Create the Domain COntroller VM (Windows Server 2022) named "DC-1". Take note of the Resource Group and the Virtual Network (Vnet) as the next VM we create will need to have these two included. 

Next we create the client VM (Windows 10) called "Client-1". Use the same RG and Vnet that was created in the DC-1 step
</p>
<br />

<p>
<img width="940" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/58e7b882-5d6c-4bef-b9a6-ae7c83113d28">

</p>
<p>
Next, we need to set the DC-1 VMs IP to static. to do that we select.
  
  1. Networking
  2. NIC
  4. IP Configurations
  5. Static
  6. Save

  
</p>
<br />

<h2>Ensure Connectivity between the client and Domain Controller</h2>


<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/c65cd381-6fa0-4025-8a05-1e20881b0329">

<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/9f49d367-0cde-4200-9e51-58f36e539b3f">


</p>
<p>
Let us now check the connection between the two VMs. Lets ping the DC-1 from Client-1. Notice how at first it says "Request timed out". That's because DC-1's firewall didn't allow for ICMP requests to come in. In order to change that, we logged into DC-1, went to the firewall settings and enabled ICMP traffic to pass through. Once enabled, then we can see ICMP replys from Client-1. Now we know that both VMs can communicate with each other. 
</p>
<br />


<h2>Install Active Directory</h2>

<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/e42c1b88-da43-4bef-b50f-dfef2c198264">

</p>
<p>
  
<h3> 1. To install Active Directory we log into DC-1</h1>
  
- Server Manager > "Add Roles and Features" > Check "Active Directory Domain Services"
</p>
<br />

<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/837c7e10-5a5c-41a4-b2ba-44a88f3f951c">

</p>
<p>

</p>
<br />

<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/fa1ab3c0-7ca6-4660-a893-509f63e51ebe">

</p>
<p>
<h3> 2. Promote to domain controller</h1

- Add a new forest called "mydomain.com" (you can call it whatever you want)                                      
</p>
<br 

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />


<h2>Create an Admin and Normal User Account in AD</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />


