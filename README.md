# Helpdesk Homelab: Windows Domain Environment

A virtual Windows domain I built to practise the day-to-day work of an IT helpdesk: managing users and groups, applying policies, controlling access to shared files, and troubleshooting sign-in problems. Each folder contains my notes, the reasoning behind each step, and screenshots.

Built in VirtualBox in October to November 2026, following the "IT Helpdesk Lab" series by KevTech IT Support, and extended with my own work on department-based shares using security groups and Group Policy drive maps and screen lock.

## Lab environment

| Component | Details |
|---|---|
| Hypervisor | Oracle VirtualBox, host-only network |
| Domain controller | Windows Server 2025 Standard Evaluation (`LDN-DC-01`), domain `yahyalab.com` |
| Client | Windows 11 (`DESKTOP01`), joined to the domain |
| Network | Static IP addresses on a private 10.x.x.x range, with the domain controller providing DNS |
| Users and groups | Users `john`, `kevin`, `james`, `susan`; security groups `IT`, `Finance`, `HR` |

## What I built

| Folder | What I did |
|---|---|
| [01-environment-setup](01-environment-setup/notes.md) | Installed VirtualBox and built the Windows Server 2025 virtual machine |
| [02-active-directory-setup](02-active-directory-setup/notes.md) | Installed Active Directory Domain Services and promoted the server to a domain controller, creating the `yahyalab.com` domain |
| [03-ad-user-accounts](03-ad-user-accounts/notes.md) | Created user accounts, set per-user logon hours, and checked accounts from the command line |
| [04-client-domain-join](04-client-domain-join/notes.md) | Built a Windows 11 client, configured static IPs and DNS, tested connectivity, joined it to the domain, and connected to the server with Remote Desktop |
| [05-password-and-lockout-policy](05-password-and-lockout-policy/notes.md) | Set the domain password and account lockout policy with Group Policy, tested the lockout, and unlocked the account |
| [06-security-groups-and-shares](06-security-groups-and-shares/notes.md) | Created department security groups and a shared folder per department, then tested allowed and denied access from the client |
| [07-group-policy-drive-maps](07-group-policy-drive-maps/notes.md) | Used Group Policy to map drives by department group and to lock idle machines |

## Skills demonstrated

- **Active Directory:** domain controller setup, user accounts, security groups
- **Group Policy:** password and lockout policy, drive maps targeted by security group, screen lock, using separate policies instead of editing the default one
- **File shares and permissions:** share and NTFS permissions, access granted to groups rather than individuals, Modify instead of Full Control
- **Networking basics:** static IP addressing, subnet masks, DNS and why Active Directory depends on it, testing with ping by IP and by name
- **Windows administration:** domain join, Remote Desktop, Active Directory Users and Computers, Server Manager
- **Command line:** `ping`, `systeminfo`, `net user`, `gpupdate`

## Problems I troubleshot

- A user couldn't sign in to the domain-joined PC because of a logon-hour restriction I had set earlier. I found the cause and removed it.
- Confirmed the lockout policy by failing five sign-ins, then unlocked the account in Active Directory.
- A screen-lock policy had no effect because the GPO was created but never linked to the domain. I linked it and retested.

## How to read this repo

Each folder has a `notes.md` with the steps I took, why I took them, and screenshots as evidence. Where something went wrong, there is a "Problems & fixes" section.
