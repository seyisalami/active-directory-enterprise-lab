# Group Policy Configuration

## Overview

```mermaid
flowchart TD
    GPMC["Group Policy Management"]

    GPMC --> Drives["GPO: Drive Mappings"]
    GPMC --> Security["GPO: Workstation Security Baseline"]
    GPMC --> RDP["GPO: Workstation RDP"]

    Drives --> Users["Users OU"]
    Security --> Computers["Workstations OU"]
    RDP --> Computers

    Users --> HR["HR Users"]
    Computers --> Client["CLIENT01"]

    HR --> Share["HR Network Drive - H:"]
    Client --> Settings["Screen Lock, Disable guest access, Auditing, Restrict RDP access..."]
```

## Validation

Ran on CLIENT01:

```powershell
gpupdate /force
gpresult /r
gpresult /r /scope computer
```

Verified that the expected GPOs were applied successfully.

## Key Takeaway
Group Policy allows administrators to distribute configurations across multiple computers without configuring each device manually.