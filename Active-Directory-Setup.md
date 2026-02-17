# ⭐ Windows Server 2025 + Windows 11 VirtualBox Lab
Basic Domain Setup & Machine Connection
This lab creates a simple domain environment using VirtualBox, Windows Server 2025, and a Windows 11 client.
The goal is only to:

Install Server 2025
Create a domain
Put both VMs on the same network
Join the Windows 11 machine to the domain

No user management, no GPOs, no advanced configuration yet.

📦 1. VirtualBox Network Configuration
Create a dedicated private network for the lab.
Steps

Open VirtualBox
Go to File → Tools → Network Manager
Add a Host‑Only Network
Recommended configuration:

Name: LAB-NET
IPv4 Address: 192.168.50.1
IPv4 Mask:    255.255.255.0
DHCP Server:  Disabled

This provides a stable LAN for your VMs.

🖥️ 2. Windows Server 2025 Desktop VM Setup
Recommended VM Settings
Name: Server
OS: Windows Server 2025
RAM: 4–8 GB
CPU: 2–4 cores
Disk: 60 GB (VDI, Dynamically Allocated)
Network Adapter 1: Host‑Only Adapter (LAB-NET)
Network Adapter 2: NAT   (optional for updates)

Install Windows normally.

<img width="1006" height="802" alt="Screenshot_2026_02_16-1" src="https://github.com/user-attachments/assets/3dc91d32-2759-4354-b87e-be6edcd81e2d" />


🌐 3. Assign Static IP to the Server
Inside Windows Server:

Open Settings → Network & Internet → Ethernet
Select the Host‑Only adapter
Click Edit under “IP Assignment”
Set to Manual → IPv4

Use:
IP Address: 192.168.50.10
Subnet Mask: 255.255.255.0
Gateway: (leave blank)
DNS: 192.168.50.10

This ensures the server will serve DNS for the domain.

🏰 4. Install Active Directory Domain Services

Open Server Manager
Select Add Roles and Features
Choose Active Directory Domain Services
Install → then click Promote this server to a domain controller
Choose:

Create a new forest
Root Domain Name: corp.local

<img width="1024" height="733" alt="Screenshot_2026_02_16-3" src="https://github.com/user-attachments/assets/13853443-964a-4468-bb37-0852b96ecf36" />

Reboot when completed.

💻 5. Windows 11 Client VM Setup
Recommended VM Settings
Name: WIN11-CLIENT
OS: Windows 11
RAM: 4 GB
CPU: 2
Disk: 40 GB
Network Adapter: Host‑Only Adapter (LAB-NET)

Install Windows normally.

🌐 6. Assign IP to Windows 11 Client
Inside Windows 11:

Control Pannel → Network & Internet → Network and Sharing Center → Change adapter settings → Properties
Select Internet Protocol Version 4(TCP/IPv4)

Set:
IP Address: 10.0.2.6
Subnet Mask: 255.255.255.0
Gateway: 10.0.2.1
DNS: 10.0.2.5  (Domain Controller)

<img width="780" height="588" alt="Screenshot_2026_02_16-4" src="https://github.com/user-attachments/assets/9f6f55c0-6575-4ad5-933f-6c61f7792340" />

🔁 7. Test Connectivity Between Server & Client
From the Server:
ping 192.168.50.20

From the Client:
ping 192.168.50.10

If both machines reply, the network is working.

🔗 8. Join Windows 11 Client to the Domain
On the Windows 11 machine:

Settings → System → About
Click Rename this PC (advanced)
Select Join a Domain
Enter the domain:

corp.local


Log in using:

Username: CORP\Administrator
Password: (Server admin password)

Restart when prompted.

✅ Lab Complete
At this stage, you have:

A functioning Windows Server 2025 domain controller
A Windows 11 client joined to the domain
Working DNS and network connectivity
Clean groundwork for future features

No unused or advanced configurations included.
