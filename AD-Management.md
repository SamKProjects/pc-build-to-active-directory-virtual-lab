# ⭐ Active Directory Essentials
OUs • User Management • Password Policy • Desktop Background (GPO)
In this document, I document the core administrative tasks I performed after building the domain:

Created a clean OU structure
Created and managed domain users
Reset user passwords
Enforced stricter password requirements
Applied a domain‑wide desktop background via GPO


📁 1) Organizational Units (OUs)
Goal: Organize objects and prepare for targeted Group Policy.
Steps I took:

Opened Server Manager → Tools → Active Directory Users and Computers (ADUC).
Right‑clicked the domain and selected New → Organizational Unit.
Created an initial structure:

CORP
 ├─ Users
 ├─ Computers
 ├─ Servers
 └─ Groups

This structure keeps users, computers, and servers separated and ready for scoped policies.

<img width="2058" height="782" alt="Screenshot_2026_02_18-2" src="https://github.com/user-attachments/assets/695c368a-0d9e-45b7-9631-8b0121081288" />

👤 2) Creating Users
Goal: Add standard domain user accounts with a consistent naming pattern.
Process I followed in ADUC:

Navigated to the Users OU.
Right‑clicked → New → User.
Entered first/last name and a logon name (e.g., jdoe, samuel.kirstein).
Set an initial (temporary) password and left “User must change password at next logon” enabled.

Example username conventions I used:
firstname.lastname
jdoe
m.smith


🔐 3) Resetting User Passwords
Goal: Provide a quick, auditable way to handle password resets.
What I did:

Located the user in ADUC.
Right‑clicked the account → Reset Password.
Entered the new password and chose whether to force a change at next logon.


🛡️ 4) Strengthening the Password Policy
Goal: Enforce stronger domain‑wide password hygiene.
Where I configured it:

Group Policy Management → Edited the Default Domain Policy
Path:

Computer Configuration
  → Policies
    → Windows Settings
      → Security Settings
        → Account Policies
          → Password Policy

Settings I applied:
Minimum password length:      12
Password must meet complexity: Enabled
Maximum password age:         30 days
Minimum password age:         1 day
Password history:             24 remembered
<img width="1021" height="773" alt="Screenshot_2026_02_18-3" src="https://github.com/user-attachments/assets/485c77bc-1102-43f3-8ab9-fda6047dc370" />

Apply/verify on a client:
PowerShellgpupdate /force``Show more lines

<img width="1006" height="759" alt="Screenshot_2026_02_18-4" src="https://github.com/user-attachments/assets/d2bfb340-cb0a-455e-8c4b-4bb0e2bde6c5" />

🖼️ 5) Domain‑Wide Desktop Background (GPO)
Goal: Standardize the desktop background for branding and easy domain identification.
Preparation I did:

Created a shared, highly available path in SYSVOL or NETLOGON (replicated across DCs).

Example:
C:\Windows\SYSVOL\domain\scripts\Wallpapers

or
C:\NETLOGON\Wallpapers




Placed the image file there (e.g., CorpWallpaper.jpg).
Ensured Domain Users have read permissions.

GPO I created and configured:

In Group Policy Management, I created a new GPO linked at the domain level:
Name: Corp Desktop Background


Edited the GPO and set:
User Configuration
  → Policies
    → Administrative Templates
      → Desktop
        → Desktop
          → Desktop Wallpaper = Enabled
          → Wallpaper Name = \\corp.local\NETLOGON\Wallpapers\CorpWallpaper.jpg
          → Wallpaper Style = Fill


Applied it on a Windows 11 client:
PowerShellgpupdate /forceShow more lines

Signed out/in to confirm the wallpaper change.


Tip: Using the UNC path under \\<domain>\NETLOGON\… or \\<domain>\SYSVOL\… ensures the file is available on any DC via DFS replication.


✅ Outcome
By the end of these steps, I:

Established a clear OU hierarchy for scalable administration.
Created domain users with consistent naming and secure onboarding.
Implemented a reliable password reset process.
Enforced stronger password policy at the domain level.
Deployed a standard desktop wallpaper across domain users via GPO.
