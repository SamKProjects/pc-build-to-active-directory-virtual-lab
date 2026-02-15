# 🧰 BIOS Configuration & Windows 11 Installation
This document covers the complete setup process used for the IT lab environment, including configuring BIOS settings (virtualization, XMP, boot order) and installing Windows 11 from a bootable USB created with Rufus.

🔧 1. Enter BIOS

Restart the PC
Press DEL on startup (Gigabyte boards)
Enter Advanced Mode using F2


⚙️ 2. Enable Virtualization (SVM Mode)
Required for Hyper‑V, VirtualBox, VMware, and running multiple VMs.
Gigabyte B450M DS3H V2 Path:

M.I.T. → Advanced CPU Settings → SVM Mode → Enabled


🚀 3. Enable XMP for RAM Performance
Enabling XMP ensures RAM (48GB total) runs at proper speeds.
Path:

M.I.T. → Advanced Memory Settings → X.M.P. → Profile 1


🔄 4. Set USB as Primary Boot Device
Needed to load the Windows installer from Rufus USB.
Steps:

Go to BIOS → Boot
Set Boot Option #1 = USB drive
Press F10 to save and reboot


💾 5. Create Windows 11 Bootable USB (Rufus)
Requirements

Windows 11 ISO
Rufus application
8GB+ USB drive

Steps

Open Rufus
Select USB drive
Choose the Windows 11 ISO
Use the following settings:

Partition Scheme: GPT
Target system: UEFI
File System: NTFS


Click Start
Wait for Rufus to finish creating the bootable USB


🪟 6. Install Windows 11

Boot PC → BIOS shows USB as Boot Option #1
The Windows installer loads
Select:

Language
Region
Keyboard layout


Click Install Now
Select I don’t have a product key (optional)
Choose Windows 11 Pro (best for IT labs)
Choose Custom Installation
Select SSD (500GB)
Click Next and allow Windows to install
PC will reboot several times


🖥️ 7. Complete Windows Setup (OOBE)

Create a local user account
Configure privacy settings
Let Windows load to the desktop
Install updates
Install chipset, LAN, and GPU drivers
Prepare the system for virtualization and lab work


🎯 Final Purpose
These combined steps ensure:

BIOS is optimized for virtualization
RAM runs at correct speeds with XMP
System boots properly from USB
Clean Windows 11 environment is installed
Machine is fully ready for virtual machines and Active Directory lab setup
Ideal base for help desk, IT support, and system admin training
