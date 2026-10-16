# File Services and Permissions

## Overview

```mermaid
flowchart TD
    SRV01[SRV01 File Server]
    SRV01 --> Shares[D:\Shares]

    Shares --> HR[HR]
    Shares --> Finance[Finance]
    Shares --> IT[IT]
    Shares --> Public[Public]

    GGHR[GG_HR_Users] --> DLHR[DL_HR_RW]
    GGFIN[GG_Finance_Users] --> DLFIN[DL_Finance_RW]
    GGIT[GG_IT_Users] --> DLIT[DL_IT_RW]

    DLHR -->|Modify| HR
    DLFIN -->|Modify| Finance
    DLIT -->|Modify| IT
```

SRV01 will provide centralized file sharing with access controlled through Active Directory security groups.

## Planned Configuration

```text
D:\Shares
├── HR
├── Finance
├── IT
└── Public
```

### Permissions

| Folder | Security Group | NTFS Permission |
|---|---|---|
| HR | DL_HR_RW | Modify |
| Finance | DL_Finance_RW | Modify |
| IT | DL_IT_RW | Modify |
| Public | Authorized users | Read |

SMB share permissions and NTFS permissions were configured to ensure departmental access.

## Validation

From CLIENT01:
- HR users could access `\\SRV01\HR`.
- Finance users were denied access to the HR share.
- Authorized users were able to create and modify files in their respective departmental shares.

## Key Takeaway
Combining AD security groups with SMB and NTFS permissions enables centralized, role-based access to shared resources.