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

<h2>Deployment and Configuration Steps</h2>
In this lab, we will create two VMs in the same virtual network. One will be a Domain Controller, the other will be a Client machine. The first thing you will be doing is creating a resource group within the Azure Portal. By searching up resource group in the search bar in the Azure Portal and selecting create. Name the resource group 'Active-Directory-Lab', and for the region, select US East 2, and click create.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Afterwards, you have to create a virtual network by sure for it in the search bar with the Azure portal and selecting create. For the resource group, select Active-Directory-VNet through the drop-down arrow and name the virtual Network Active-Directory-Lab. Then set the region to (US) East US 2 and select Review + create 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now you'll have to create a VM by searching for it and clicking create. For the resource group, select Active-Directory-Lab and the VM name, set it as dc-1. Then set the region to the same region as your Virtual network, which is (US) East US 2. Now for the image select Windows Server 2022 Datacenter: Azure Edition -x64 Gen2 and for size select anything with at least 2cpus. Then, for the username, set it as labuser and the password as Cyberlab123!, and next, check off both boxes for the licensing agreement. When your done select next and click next for Disks. Now in the Networking tab for VN make sure it's Active-Directory-VNet and the subnet is set to default, and leave the reset and click create.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, create the Client VM by following the same steps as the previous step, making the image (Windows 10 Pro) and naming the VM “Client-1.” Then, set the username as labuser and the password as Cyberlab123!
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After DC-1 is created, set the Domain Controller’s NIC Private IP address to be static. You'll do that by going to virtual machines and selecting dc-1, and on that page, click networking -> Network settings -> Network interface/ IP configuration -> ipconfig 1. Then, under Private IP address settings, select static and hit save.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, you'll have to log into the VM and disable the Windows Firewall (for testing connectivity). First, you will have to get dc-1 public IP address and connect to it with Microsoft Remote Desktop on either Windows or Mac, and put in the username and password we set earlier for dc-1 VM. Once you log in, right-click the Start menu and select Run and type wf.msc and press Enter. Then select Windows Defender Firewall Properties and go to Domain profile and private profile, and where it says Firewall state select off and click apply and ok to save.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After that,  set Client-1’s DNS settings to DC-1’s Private IP address. You'll do that by copying dc-1 IP address and clicking on Client-1, and selecting networking -> network settings -> Network interface/ IP configuration -> DNS Servers. Then, under DNS server type in dc-1 private IP address and hit save.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the Azure Portal, restart Client-1 -> Login to Client-1 -> Attempt to ping DC-1’s private IP address and ensure the ping succeeded -> From Client-1, open PowerShell and run ipconfig /all, and the output for the DNS settings should show DC-1’s private IP Address.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
