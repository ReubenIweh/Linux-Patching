 📑 **Table of Contents**
 
- [Patching Schedule](#patching-schedule)
  
- [Pre-Patching Preparation](#pre-patching-preparation)
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


**Notify Users / Plan Downtime: Send email or Slack notification to teams.**

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

Check Current Kernel and Package Versions
- `uname -r`
- `rpm -qa --last`   # RHEL/CentOS
- `dpkg -l`          # Debian/Ubuntu

Checking available updates:
- `sudo apt update`            # For Debian-based systems (Ubuntu, etc.)
- `sudo yum check-update`      # For Red Hat-based systems (CentOS, RHEL, Fedora)

Check Uptime:
- `uptime`

Check disk space to ensure there’s enough room for patches:
- `du -hT`

Verify running services and their health (e.g., web server, database):

- `systemctl status httpd    # For Apache web server`
- `systemctl status mysql    # For MySQL`

  ## During Patching

**RHEL/CentOS**

- `yum check-update`
- `sudo yum update -y`

**For Debian/Ubuntu-based systems:**
- `sudo apt upgrade`
- `sudo apt dist-upgrade  # For upgrading distribution packages`

  **Verify Patch Installation:**

To ensure that patches have been applied successfully, check the versions of the updated packages:

- `dpkg -l | grep [package-name]  # For Debian/Ubuntu`
- `rpm -qa | grep [package-name]  # For Red Hat/CentOS`

