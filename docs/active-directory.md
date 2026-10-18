# Active Directory Management

## Overview

```mermaid
flowchart TD
    Domain[corp.adlab.test]
    Domain --> Corp[Corp]

    Corp --> Users[Users]
    Users --> IT[IT]
    Users --> HR[HR]
    Users --> Finance[Finance]
    Users --> Management[Management]

    Corp --> Computers[Computers]
    Computers --> Workstations[Workstations]
    Computers --> Servers[Servers]

    Corp --> Groups[Groups]
    Corp --> AdminAccounts[Admin Accounts]
    Corp --> ServiceAccounts[Service Accounts]
```

Active Directory is used to centrally manage users, computers, and security groups in the `corp.adlab.test` domain.

![OU structure in Active Directory Users and Computers](../screenshots/active-directory/active-directory-OU.png)

## Configuration
- Created departmental OUs for IT, HR, Finance, and Management.
- Created domain users using PowerShell and a CSV file.
- Implemented security groups to manage departmental access.

### Security Groups

All groups are stored in the [Corp\Groups](../screenshots/security/security_groups.png) OU.

| Global Group | Domain Local Group | Resource |
|---|---|---|
| GG_HR_Users | DL_HR_RW | `\\SRV01\HR` |
| GG_Finance_Users | DL_Finance_RW | `\\SRV01\Finance` |
| GG_IT_Users | DL_IT_RW | `\\SRV01\IT` |

This lab implements the **AGDLP** model:

```mermaid
flowchart LR
    User[User Account<br>jbrown]
    GG[GG_Finance_Users<br>Global Group]
    DL[DL_Finance_RW<br>Domain Local Group]
    Resource[Finance Share<br>\\SRV01\Finance]

    User --> GG
    GG --> DL
    DL -->|Modify| Resource
```

Accounts → Global Groups → Domain Local Groups → Permissions

Users were added to their department's global group, and only the domain local group is granted permissions on the resource:

![Adding users to a departmental global group](../screenshots/security/group_assignment.png)

## Validation

```powershell
Get-ADUser -Filter *
Get-ADGroupMember -Identity "GG_Finance_Users"
```

## Key Takeaway
Security groups simplify permission management by assigning access to groups instead of individual users.