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

<h2>Step 1 — In Microsoft Azure Portal:</h2>

- Create a Resource Group
- Create a Virtual Network:
Example:
VNet: LabNetwork


<h2> Step 2 - Create the Domain Controller VM</h2>

- In Microsoft Azure Portal:

→ Create VM

OS: Windows Server 2022

Name: DC1

Size: B2s (fine for labs)

Username/password: create admin credentials

Subnet: default

<h2>Step 3 — Set Static Private IP</h2>

- After the VM deploys:

Go To:

- DC1 → Networking → Network Interface → IP Configurations

Change:

- Allocation: Dynamic → Static

- Save changes.

- This is important because clients must always find the domain controller at the same IP.

<h2>Step 3 — Create Client VM</h2>

- In Microsoft Azure Portal:

→ Create VM

OS Windows 10/11 VM

Size: B2s (fine for labs)

Username/password: create client credentials

Set VNet to the same as DC1

Subnet: default


IMPORTANT:

The client VM must use the Domain Controller as DNS.

- Change DNS Server

Go to:

- Client VM → Network Interface → DNS Servers → Custom DNS

Enter:

- (Private IP of DC1)

Save → Restart the client VM.

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
- Restart the DC1 VM

<h2>Step 5 — Create the Domain</h2>

Choose:

- Add a new forest

Example domain names:

testlab.com
strakerlab.com

- Set:

DSRM password

Finish installation.

- The VM will reboot automatically.

<h2>Step 6 — Join Client to Domain</h2>

- On the client VM:

Open:
Settings → System → About → Rename this PC (Advanced)

Then:

Computer Name Tab → Change → Domain

Enter:

domain name:
Example: strakerlab.com

- When prompted:

Username:
Administrator
Password:
Use your domain admin password.
Restart the PC.

- <h2>You now have Active Directory working.</h2>

<h2>Deployment and Configuration Steps</h2>

<p><img width="1631" height="865" alt="Screenshot 2026-05-25 202014" src="https://github.com/user-attachments/assets/855207dc-c8c7-44bc-896c-cc95a690e4f1" />
<img width="1180" height="848" alt="Screenshot 2026-05-25 192902" src="https://github.com/user-attachments/assets/1720add1-2dff-4c5d-b190-51d394d2179a" />
<img width="1167" height="892" alt="Screenshot 2026-05-25 192945" src="https://github.com/user-attachments/assets/c9e494a2-a866-46a4-a712-e65fbbbb3e03" />
<img width="1630" height="899" alt="Screenshot 2026-05-25 193711" src="https://github.com/user-attachments/assets/34a88fe0-9d21-41d9-b765-78d70654b95e" />

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="1637" height="986" alt="Screenshot 2026-05-25 193835" src="https://github.com/user-attachments/assets/95df6f4c-2556-4b9e-bada-4d3547c487f7" />
<img width="1177" height="904" alt="Screenshot 2026-05-25 193422" src="https://github.com/user-attachments/assets/1442a80d-9775-41fa-862f-81d37d0994b2" />
<img width="1217" height="895" alt="Screenshot 2026-05-25 193246" src="https://github.com/user-attachments/assets/60f7790d-ddbb-4433-8f13-b025f461664e" />

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img width="4032" height="3024" alt="IMG_0038" src="https://github.com/user-attachments/assets/04fb6cbe-c62b-4fb1-9ae6-76bb6d2c2a86" />
<img width="4032" height="3024" alt="IMG_0039" src="https://github.com/user-attachments/assets/7755595b-0f27-4eac-98ff-cc00d42e29ff" />
<img width="4032" height="3024" alt="IMG_0040" src="https://github.com/user-attachments/assets/895ca4ba-f5a5-49ab-b11f-1e497e5d0031" />
<img width="4032" height="3024" alt="IMG_0041" src="https://github.com/user-attachments/assets/8763f25f-d3ea-43cc-8b3e-32f00732ca6e" />
<img width="4032" height="3024" alt="IMG_0042" src="https://github.com/user-attachments/assets/e70002e2-a297-4353-aac0-62a08dde75ba" />
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
<p>
<img width="4032" height="3024" alt="IMG_0043" src="https://github.com/user-attachments/assets/515749e9-77b9-43d5-8be9-de2bc334fa60" />
<img width="4032" height="3024" alt="IMG_0044" src="https://github.com/user-attachments/assets/37308a08-3b6c-4817-b620-6041b956c84e" />
<img width="4032" height="3024" alt="IMG_0045" src="https://github.com/user-attachments/assets/852da1a0-909c-4b6a-9908-b38f33353cec" />
<img width="4032" height="3024" alt="IMG_0046" src="https://github.com/user-attachments/assets/f697bf4e-2fd3-4a80-b067-81dc981c9471" />
<img width="4032" height="3024" alt="IMG_0047" src="https://github.com/user-attachments/assets/cd027c4b-f4b7-4ae2-9da9-599c68b49c26" />

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
