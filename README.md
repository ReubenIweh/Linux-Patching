 📑 **Table of Contents**
 
- [Patching Schedule](#patching-schedule)
  
- [Pre-Patching Preparation](#pre-patching-preparations)
 - Scheduling Patches
 - Backup
 - System Update Check
 - Check Server Health
   
- [During Patching](#during-patching)
 - Step-by-Step Patching Process
 - Commands to Run
 - Monitoring Tools
   
- [Post-Patching Actions](#Post-patching)
 - Verifying Patches
 - Rebooting the Server
 - Rollback Options
 - Troubleshooting Failures
   
- [Rollback Options](#rollback-options)
  
- [Troubleshooting Patch Failures](#troubleshooting-patch-failures)

## Patching Schedule

| Environment | Patching Schedule                                             | Notes                      |
| ----------- | ------------------------------------------------------------- | -------------------------- |
| Production  | Monthly or Quarterly, off-peak hours (e.g., weekend midnight) | Involves downtime planning |
| UAT/Staging | A few days before production                                  | Used to test patches       |
| Development | Weekly or ad-hoc                                              | Often automated            |


## Pre-Patching Preparation

Linux patches are typically scheduled based on the criticality of the patch and business requirements. A typical patching schedule looks like this:

Security patches: Applied immediately or within a few days, especially for vulnerabilities that have known exploits.

Non-security patches (feature updates): These can be scheduled for weekends or during off-peak hours, typically every second or third Friday of the month.

Best Practice: Schedule patching during off-peak hours, typically between midnight to 4 AM on weekends (if your business allows). This minimizes the impact on production systems.

**Backup the Server**

Before applying any patches, always back up your server! This can be done by creating snapshots or full backups of the system using the following commands:

- `rsync`
- `tar`
- `scp`
- `snapshot`

  Example:
  ```rsync -avz / /backup/location/```

**Check System Updates and Health**
