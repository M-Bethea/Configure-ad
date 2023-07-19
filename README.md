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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
1. Setup Resources in Azure (your resource group, VM name, region, image, size (at least 2vm's), username and password) <br>
A. Create the Domain Controller VM (Windows 10 Pro Server 2022) named “DC-1” <br>
i. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time <br>
</p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/9cf11a9f-314e-42f9-867e-df8b79aba675" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/afd3b375-aed3-4217-9f78-839ed9282b79" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

B. Set Domain Controller’s NIC Private IP address to be static <br>
i. Go back to the home page -> Got your Network Interface -> IP Configurations -> ipconfig -> Static -> Save. Keep everything as is, except the allocation
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/7c853e21-6281-4636-a368-a365fc9691a3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

C . Create the Client VM (Windows Pro 10) named “Client-1”. Use the same Resource Group and Vnet that was created for DC-1 <br>
i. Make sure both VMs are in the same Vnet (you can check with Network Watcher), use the same same number of vm's (two in this case) and region,  create your username and password and checkmark the licensing box. <br>
</p>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/daad9b29-125d-4c2b-85b9-b8331a62a3d6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
2. Ensure Connectivity between the client and Domain Controller <br>
A. Login to Client-1 with Remote Desktop using the public IP address and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping) using the command line -> start -> CMD <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/682857c4-f4e9-444e-9132-aac9c7d9ee37 height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

B. Login to the Domain Controller (DC-1) and enable ICMPv4 on the local windows Firewall <br>
i. start -> wf.msc ->
ii. Inbound Rules -> Click "Protocol" and look for ICMPv4 -> Enable: Core Network Diagnostics (private) and Core Network Diagnostics (Domain)
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/ac84bc04-6494-4154-97b1-5fbba85b6397" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/3e75d2da-967e-4321-a02b-cc08f95941bd" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p

C. Check back at Client-1 to see the ping succeed
i. Press ctrl + C to end the ping
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/984000e6-afe3-4a9c-a827-f80d6abb3fb3 height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br />

<p>
3. Install Active Directory
A. Login to DC-1 and install Active Directory Domain Services
i. In the Server Manager, Add "Roles and Features", Select next until you get to "Server Roles", Check "Active Directory Domain Services" -> Add Features -> Keep clicking next until you can install
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/ffbf8f9d-5c96-4bee-a7fe-65f8ac00ad8b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
B. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is) <br>
i. Click the flag and promote this server to a domain controller <br>
ii. Make a password and next through until you can install <br>
iii. The VM may shut itself down
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/3e1cc858-113a-44c0-a34a-4b674cfcf394" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/38a94a6e-fa01-4e2b-b5ca-9ab19d21f1fa" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
C. Restart and/or log back into DC-1 as [user: mydomain.com\labuser] (your username)
</p>
<br />

<p>
4. Create an Admin and Normal User Account in AD: Tools -> Active Directory Users and Computers -> Right click mydomain.com(or your username) -> New -> Organizational Unit 
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/543728a9-a342-416f-a9bd-a7f67d5904ee" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
A. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”  <br>
i. Create a new OU named “_ADMINS” <br>
B. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”: Admins -> New -> User <br>
i. Uncheck "user must change password" and check "password never expires" <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/81be2e87-e57a-4b9d-8844-18934521a9f1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
ii. Add jane_admin to the “Domain Admins” Security Group: Right Click "jane_admin" -> Properties -> Member Of -> Add -> Domain -> Check Names -> Domain Admins -> OK -> Apply -> OK <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/58bb3b11-a7a8-400f-8453-5ff6a4541186" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
C. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin” <br>
i. Use user jane_admin as your admin account from now on 
</p>
<br />


<p>
5. From the Azure Portal, set Client-1’s DNS settings to the Domain Controllers (DC’s) Private IP address <br>
A. Can scroll down or got to networking and you'll see "NIC Private IP" <br>
i. Go to Client-1 -> Networking -> Network Interface -> DNS Servers -> Custom -> DC-1's Private IP -> Save
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/4dbd8b66-40fa-45b5-bf3c-aa1ce9f9b52d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/0f83bff0-21dc-404d-9a15-4e35e03caa71" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
ii. From the Azure Portal, restart Client-1 <br>
B. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart) <br>
i. Type ipconfig /all to check DNS server
ii. Ping the DNS Server, should get a reply
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/4df4da66-3186-4bc2-960e-b32185b7847b height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
C. Join Client-1 to your domain (mydomain.com) <br>
i. Start -> Setting -> System -> About -> Rename this PC Advanced -> Change -> Domain: mydomain.com (or your domain) -> OK
ii. If prompted for username and password: username mydomain.com\jane_admin and your password -> OK
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/4289ffc3-707a-4325-bd03-d9a97ff9501c height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
D. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain <br>
E. Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes.)
<p>
<br />

<p>
A. Setup Remote Desktop for non-administrative users on Client-1 <br>
B. Log into Client-1 as mydomain.com\jane_admin and open system properties <br>
i. System -> Remote Desktop -> Select Users that Can Remotely Access this PC -> Add -> domain users -> Check Names -> OK -> OK <br>
B. You can now log into Client-1 as a normal, non-administrative user now <br>
C. Normally you’d want to do this with Group Policy that allows you to change many systems at once
</p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/a1524939-260d-4262-9989-0c30c04e7fa9" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
6. Create a bunch of additional users and attempt to log into client-1 with one of the users <br>
A. Login to DC-1 as jane_admin <br>
B. Open "PowerShell_ise" as an administrator <br>
i. Right click -> Open as Administrator
C. Create a new File and paste the contents of the <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1/">script</a> into it  <br>
i. Run the script and observe the accounts being created <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/ca9dc35f-b4cf-41ce-8705-192ed8636345" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
D. When finished, open ADUC and observe the accounts in the appropriate OU <br>
i. Right click and Refresh "_EMPLOYEES" <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/57fdcbfd-74e8-4859-82d7-8ff9d5805b0c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
E. Attempt to log into Client-1 with one of the accounts (take note of the password in the script: Password1) <br>
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/1cda88e7-e517-42fc-a510-20d6564c3fd3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/4b886e4d-bc1c-44c0-8b4f-f664968f1b4e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<p>
  <img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/dfc643fa-3555-4870-8e98-58a74b9d2ceb height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

