<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-site Active Directory setup using Azure</h1>

Outline of how to setup an Active Directory using Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computers)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>Step 1 — Create a Resource Group and VNet</h2>

- In Microsoft Azure Portal:

Click on <b>Resource Group</b> → Create → name your Resource Group

Example: TestRG

<p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/7eb2a020-40a3-44af-abd1-37ea21741158" />
</p>

Then:

- Create a Virtual Network (VNet):

Click on <b>Virtual Network</b> → Create → name your VNet

Example VNet: TEST

<p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/2cfef8ad-5f09-4740-9cb5-68376120dd8b" />
</p>

<h2> Step 2 - Create the Domain Controller VM</h2>

In Microsoft Azure Portal:

Go to <b> Virtual Machines</b> → Create

Create VM:

- Resource Group

Example: Test

- OS: Windows Server 2022

- Name: Name of your choice

Example: DC1

- Size: B2s (fine for labs)

- Username/password: create admin credentials

- VNet: TEST

<p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/e414edbd-970e-4785-a1cd-f3fc46b59049" />

</p>

<p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/af07c7ab-dfd5-4161-b164-b901eb46ae56" />
</p>

<h2>Step 3 — Set Static Private IP</h2>

After the VM deploys go to:

- Virtual Machine → DC1 → Networking → Network Interface → IP Configurations

Change:

- Allocation: Dynamic → Static → Save changes

- This is important because clients must always find the domain controller at the same IP.

<p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/2b2d0546-bb4a-48c7-8235-1d3b90f2168f" />

</p>

<h2>Step 4 — Create Client VM</h2>

In Microsoft Azure Portal:

Go to <b> Virtual Machines</b> → Create

- Resource Group should be the same as DC1's

Example: TestRG

- OS Windows 10/11 VM

- Size: B2s (fine for labs)

- Username/password: create client credentials

- Set VNet to TEST (same as DC1)

<b>IMPORTANT:</b>

- The Client VM must use the Domain Controller as DNS.

p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/77b82461-e420-4498-83b0-7ed7fd1251bc" />

</p>

<h2>Step 5 — Change Client DNS Server</h2>

Go to:

- Client VM → Networking → Network Setting → Network Interface → DNS Servers → Custom DNS → DC1's Private IP

- Save → Restart the Client VM.

p><img width="700" height="450" alt="image" src="https://github.com/user-attachments/assets/841ce39a-4c2c-48a4-bdc9-806267dad097" />

</p>
<h2>Step 6 — Install Active Directory Domain Services</h2>

- Connect to DC1 using Remote Desktop (RDP).

Open RDP:

- In the Windows search bar on your taskbar, type Remote Desktop Connection and press Enter.

- Input DC1's public IP address → Input your DC1 username and password → connect

Open:

- Server Manager

→ Add Roles and Features → Check Active Directory Domain Services (AD DS) → click next until Install

After install finishes click:

- <b>“Promote this server to a domain controller”</b>

Add a new forest → Input Domain Name

Example Domain name: Testlab.com

Click Next → create a password → click next until Install → DC1 PC will restart automatically

- Log into DC1 with domain credentials and password

Example:

Testlab.com\username (domain admin)

<p><img width="1328" height="773" alt="image" src="https://github.com/user-attachments/assets/e292cf40-4c65-4cf4-be50-9d4df815683d" /></p>

  
<p><img width="700" height="953" alt="image" src="https://github.com/user-attachments/assets/3cfac873-dbde-4d1c-9612-a0dc3a3db857" />
</p>
<h2>Step 7 — Join Client to Domain</h2>

- On the Client VM:

Open:
Settings → System → About → Rename this PC (Advanced)

Computer Name Tab → Change → Domain

Enter domain name:

-Example: Testlab.com

- When prompted:

Username and Password

Example: Testlab.com\username (domain admin) 

Password: Use the domain admin password.

- Restart the PC.

<p><img width="700" height="953" alt="image" src="https://github.com/user-attachments/assets/af3e1630-f7aa-4137-a450-83e9de67a972" />
</p>

- <h2>You now have Active Directory working.</h2>

