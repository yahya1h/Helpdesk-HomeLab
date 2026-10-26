# Helpdesk Home-Lab

A virtualized enterprise environment built to practise core helpdesk and desktop support work: user and device administration, endpoint management, patching, and incident handling.

## Architecture

```mermaid
flowchart LR
    DC["DC-01<br/>Windows Server 2025<br/>Active Directory"]
    W11["Windows 11 Client"]
    INTUNE["Microsoft Intune"]
    PATCH["Patch Management"]
    TICKET["Ticketing System"]

    DC --- W11
    DC --- INTUNE
    PATCH -.-> W11
    TICKET -.-> DC
    TICKET -.-> W11
```

## What I Built

- **Active Directory:** configured users, groups, and OUs on a Windows Server 2025 domain controller and joined a Windows 11 client to the domain
- **Intune:** enrolled the client and applied compliance policies and app deployment
- **Patch management:** deployed and verified updates on the client using [tool]
- **Ticketing:** logged and resolved simulated incidents in [tool], documented in [`tickets/`](tickets/)

## Skills Demonstrated

Active Directory administration, Intune/MDM, patch management, ticket documentation, troubleshooting methodology

## Structure

```
├── docs/       # step-by-step build notes
├── tickets/    # incident write-ups
└── images/     # screenshots
```
