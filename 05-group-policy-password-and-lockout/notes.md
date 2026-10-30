# Group Policy: Password and Account Lockout Policy

**Objective:** Use Group Policy to set the domain's password and account lockout rules centrally, then test that the lockout works and unlock the account.

## Steps
1. On the server, opened Server Manager → Tools → Group Policy Management and expanded the forest to the `yahyalab.com` domain.
2. Right-clicked **Default Domain Policy** and selected Edit. This policy applies to every user and computer in the domain, and password and lockout rules for domain accounts are set here.
3. Went to Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy and changed **Maximum password age** from the default 42 days to 90 days, so users aren't forced to change passwords as often.
4. Went to Account Lockout Policy and set **Account lockout threshold** to 5 invalid attempts and **Account lockout duration** to 360 minutes. After 5 wrong passwords the account locks, which slows brute-force password guessing.
5. Checked the result in Group Policy Management, on the Settings tab of the Default Domain Policy.

<img src="05-gpomanagementverify.png" alt="Default Domain Policy settings showing 90-day maximum password age and account lockout after 5 invalid attempts for 360 minutes" width="600">

6. Verified the policy works by entering a wrong password for the domain user `kevin` five times on DESKTOP01. The sign-in screen then reported that the account was locked out.

<img src="05-account-lockout-kevin.png" alt="Windows 11 sign-in screen showing that Kevin's account is currently locked out" width="600">

7. Unlocked the account on the server: Active Directory Users and Computers → Users → kevin → Properties → Account tab → ticked **Unlock account** → OK. Because the lockout duration is 360 minutes, an administrator has to unlock the account manually, otherwise the user waits six hours.

## Tools / tech used
- Group Policy Management
- Active Directory Users and Computers
- Windows Server 2025 Standard Evaluation
- Windows 11 client (DESKTOP01)

## What I learned
- Group Policy applies settings centrally, so one change covers every account and machine in the domain instead of being repeated per PC.
- Domain-wide password and lockout rules belong in the Default Domain Policy, and they apply to domain accounts only, not to local accounts on a machine.
- Lockout settings trade security against support load. A long lockout duration frustrates brute-force attempts but means users who mistype their password need a helpdesk unlock.
- A locked account is unlocked in Active Directory Users and Computers on the account's Account tab, which is one of the most common helpdesk tasks.
