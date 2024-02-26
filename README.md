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
- Join Client-1 to  your Domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users using Powershell

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
<h3> 2. Promote to domain controller</h3>

- Add a new forest called "mydomain.com" (you can call it whatever you want)                                      
</p>
<br 

<p>
<img width="338" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/d251d9d2-f9bf-4cb0-a603-74e5eb6caaf4">

</p>
<p></p>



<h3> 3. Restart and then log back into DC-1 as user: mydomain.com\labuser</h3>


</p>
<br />



<h2>Create an Admin and Normal User Account in AD</h2>

<p>
<img width="718" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/3d5a577b-b778-4bea-bf66-60f3d47c3ac1">

</p>
<p>
In DC-1 go to.
  
- AD Users and Computers > mydomain.com > New > Organizational Unit > and create two OUs called "_EMPLOYEES" and "_ADMINS"  
  
</p>
<br />

<p>
<img width="721" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/99ab9482-4218-4844-92c2-bf91851425d8">

</p>
<p>
In the _ADMINS folder, create a new user named "jane doe" 
</p>
<br />

<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
To make the user an actual admin user, we must assign them to the admin group. In order to do that we must:

- Right click user > Properties > Member Of > Enter "Domain Admins" > Check Names > OK

</p>
<br />

<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/8cc9b376-4ddd-4ca5-8e52-04c7c223d13a">


</p>
<p>
After creating the account, log in as jane_admin. We will use this account as the admin account


</p>
<br />


<h2>Join Client-1 to  your Domain</h2>


<p>
<img width="719" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/0f31fc1a-48eb-4213-93ed-b75cb602189c">


</p>
<p>
To add Client-1 to our domain we must go to:

1. Setting (About this PC)
2. Rename this PC (advanced)
3. Change
4. Under "Domain" enter in your domain name
5. Enter in your admin credentials and click OK

If successful you'll get a message saying "Welcome to the mydomain.com domain".

</p>
<br />

<h2>Setup Remote Desktop for non-administrative users on Client-1</h2>

<p>
<img width="718" alt="image" src="https://github.com/PradoJuanPablo/configure-ad/assets/160810181/f01c02cc-9304-489f-80de-18dcf3b48e35">


</p>
<p>
Next we're going to allow users to be able to log into Client-1. To do what we.

1. Setting (About this PC)
2. Remote Desktop
3. Select users that can remotely access this PC
4. Add
5. Enter in "Domain Users" > Check Names > OK

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<h2>Create a bunch of additional users using Powershell</h2>

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />

<p>
<img width="719" your image 60810181/712d885c-1014-44e0-80ce-79afb4c9e33e">

</p>
<p>
Enter your text here!

- Enter your text here!

</p>
<br />




