<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-site Active Directory setup using Azure</h1>
This tutorial outlines the utilization of an on-site Active Directory using Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computers)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Configuration Steps</h2>

<h2>Step 1 — Create the Domain Controller VM</h2>

- In Microsoft Azure Portal:

Create VM
OS: Windows Server 2022
Name: DC1
Size: B2s (fine for labs)
Username/password: create admin credentials
Virtual Network:
Create new VNet
Example:
VNet: LabNetwork
Subnet: default

<h2>Step 2 — Set Static Private IP</h2>

- After the VM deploys:

Go To:

- DC01 → Networking → Network Interface → IP Configurations

Change:

- Allocation: Dynamic → Static

- Save changes.

- This is important because clients must always find the domain controller at the same IP.

<h2>Step 3 — Create Client VM</h2>

- Create your Windows 10/11 VM.

IMPORTANT:

The client VM must use the Domain Controller as DNS.

- Change DNS Server

Go to:

- Client VM → Network Interface → DNS Servers

Set:

- Custom DNS

Enter:

- (Private IP of DC1)

Save.

- Restart the client VM.
<h2>Step 4 — Install Active Directory Domain Services</h2>

- Connect to DC1 using Remote Desktop (RDP).

Open:

- Server Manager

→ Add Roles and Features

Install:

- Active Directory Domain Services (AD DS)

- After install finishes:

Click:

- “Promote this server to a domain controller”

<h2>Step 5 — Create the Domain</h2>

Choose:

- Add a new forest

Example domain names:

testlab.com
strakerlab.com

Example:

strakerlab.com

- Set:

DSRM password

Finish installation.

- The VM will reboot automatically.

<h2>Step 6 — Join Client to Domain</h2>

- On the client VM:

Open:
Settings → System → About → Rename this PC (Advanced)

OR:

sysdm.cpl

Then:

Computer Name Tab

→ Change
→ Domain

Enter:

strakerlab.com

- When prompted:

Username:
Administrator
Password:
Use your domain admin password.
Restart the PC.

- <h2>You now have Active Directory working.</h2>

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1480" height="1063" alt="image" src="https://github.com/user-attachments/assets/36961c5d-2264-4082-bd18-2d4da593b5b0" />
<img width="1486" height="1058" alt="image" src="https://github.com/user-attachments/assets/a5109496-fde8-4341-b55c-b1035b916a85" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/b17bdf04-f01e-4269-8d89-50f446ef1726" />
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/dc0443be-8722-4eb2-85c4-4e4b2b5822d3" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/1e022676-12f8-463e-b13c-f3e42ac0e2e3" />

</p>
<p>
