# Group Policy Configuration

## Overview
Group Policy is used to centrally manage workstation settings, security configurations, and access to shared resources.

## Planned Configurations

| GPO | Purpose |
|---|---|
| GPO-Drive-Mappings | Automatically map departmental network drives |
| GPO-Workstation-Security-Baseline | Configure screen lock and auditing |
| GPO-Workstation-RDP | Restrict Remote Desktop access |

Policies will be linked to the appropriate user or computer OUs.

## Validation

Ran on CLIENT01:

```powershell
gpupdate /force
gpresult /r
gpresult /r /scope computer
```

Verify that the expected GPOs apply successfully.

## Key Takeaway
Group Policy allows administrators to distribute configurations across multiple computers without configuring each device manually.