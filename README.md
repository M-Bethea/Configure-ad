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
<p>
<img src="https://github.com/M-Bethea/Configure-ad/assets/139162550/984000e6-afe3-4a9c-a827-f80d6abb3fb3 height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
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
</p><p>

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
