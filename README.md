# veeam_setup
![Ansible Lint](https://github.com/vMarkusK/veeam_setup/workflows/Ansible%20Lint/badge.svg)

An Ansible Role to install and update [Veeam](https://www.veeam.com) components (Veeam Backup & Replication / Veeam ONE) on Windows.

## Release Notes

### Version 0.1

- one_setup - Version 0.1

- one_update - Version 0.1

- vbr_setup - Version 0.1

- vbr_update - Version 0.1

### Version 0.2
- one_setup - Version 0.2
  - Strict Windows Firewall configuration (instead of disabling)

### Version 0.3
- vbr_download - Version 0.1
  - Add new Role Task to Download and Mount VBR ISO File

### Version 0.4
- vbr_setup - Version 0.2
  - Modified für v10 RTM

- one_setup - Version 0.3
  - Modified für v10 RTM

### Version 0.5
- vbr_setup - Version 0.3
  - Creates an additional Service and RunAs User
  - Run SQL Express Setup in RunAs-Mode

- one_setup - Version 0.4
  - Run SQL Express Setup in RunAs-Mode

### Version 0.6
- vbr_setup - Version 0.4
  - License File can be applied during setup

### Version 0.7
- one_setup - Version 0.5
  - License File can be applied during setup

### Version 0.8
- one_setup - Version 0.6
  - SQL Setup is optionally
  - SQL Instance can be configured (e.g. Remote SQL Server)
  - Minor Debug enhancements

- vbr_setup - Version 0.5
  - SQL Setup is optionally
  - SQL Instance can be configured (e.g. Remote SQL Server)
  - Minor Debug enhancements

- vbr_download - Version 0.2
  - Add Debug
  - v10 GA ISO and Checksum in the defaults

### Version 0.9
- vbr_update - Version 0.2
  - Latest Patch

- General 
  - Fix sime Lint findings

## Requirements

### Hardware 

CPU: x86-64 processor

Memory: 2 GB RAM

Disk Space: 500 MB for product installation and 4 GB for optional ISO Download.

Network: 1 Mbps connection to the backup server

## OS

Only 64-bit version of the following operating systems are supported:

- Microsoft Windows Server 2016
- Microsoft Windows Server 2012 R2
- Microsoft Windows Server 2019 (Tested with this Role)
- Microsoft Windows Server 2012
- Microsoft Windows Server 2008 R2 SP1
- Microsoft Windows 10 (version 1607 to 1909)
- Microsoft Windows 8.1
- Microsoft Windows 7 SP1

#### Pre Windows 2019 requirements

This role does not cover the Setup os these Veeam Backup & Replication 10 requirements:

- Microsoft .NET Framework 4.7.2 (included in the ISO)
- Windows Installer 4.5 (included in the ISO)
- Microsoft PowerShell 2.0 (included in the ISO)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
---
# defaults file for veeam_setup

## Choose Setup
vbr_download: false
vbr_license: false
vbr_setup: false
vbr_update: false
one_setup: false
one_license: false
one_update: false

## VBR Parameters
one_source: "E:\\"
one_destination: "C:\\install\\"
one_destination_license: "license.lic"
one_source_license: "/data/license.lic"
one_username: "svc_one"
one_userpassword: "ChangeM3!"
one_update_file: "" #VeeamONE_9.5.4.4587_Update#4a.exe
one_update_id: "" #Veeam ONE Update 4a
vbr_url: "https://download2.veeam.com/VeeamBackup&Replication_10.0.0.4461.iso"
vbr_checksum: "26ddcc3df046af1ca1458b3040fc9024b4361ae1e51e1cf4516afe53fb024650"
vbr_destination: "C:\\install\\"
vbr_destination_file: "vbr.iso"
vbr_destination_license: "license.lic"
vbr_source_license: "/data/license.lic"
vbr_source: "D:\\"
vbr_username: "svc_vbr"
vbr_userpassword: "ChangeM3!"
vbr_update_file: "veeam_backup_10.0.0.4461.CumulativePatch_KB3161.exe" #veeam_backup_9.5.4.2866.update4b_setup.exe
vbr_update_id: "KB3161" #Veeam VBR Update 4b
sql_setup: true
sql_instance: "(local)\\VEEAMSQL2016"
sql_username: "svc_sql"
sql_userpassword: "ChangeM3!"
sql_sapassword: "ChangeM3!"
```

## Dependencies

none

## Example Playbook

### Veeam Backup & Replication Setup with local Download

```yaml
- name: Veeam Backup & Replication v10 Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: false
    vbr_setup: true
    vbr_license: true
    vbr_source_license: "/root/ansible/license.lic"
    vbr_source: "E:\\"
    vbr_update: true
    one_setup: false
    one_source: "D:\\"
    one_update: false
  roles:
    - veeam_setup
```

### Veeam Backup & Replication Community Edition Setup with local Download

```yaml
- name: Veeam Backup & Replication v10 Community Edition Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: true
    vbr_setup: true
    vbr_license: false
    vbr_update: false
    one_setup: false
    one_update: false
  roles:
    - veeam_setup
```

### Veeam Backup & Replication Community Edition Setup with local Download and remote SQL

```yaml
- name: Veeam Backup & Replication v10 Community Edition Setup with remote SQL
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: true
    vbr_setup: true
    vbr_license: false
    vbr_update: false
    sql_setup: false
    sql_instance: "SQL001\\VEEAM"
    one_setup: false
    one_update: false
  roles:
    - veeam_setup
```

### Veeam Backup & Replication Community Edition Setup without local Download

```yaml
- name: Veeam Backup & Replication v10 Community Edition Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: false
    vbr_setup: true
    vbr_license: false
    vbr_update: false
    one_setup: false
    one_update: false
  roles:
    - veeam_setup
```

### Veeam ONE Setup

```yaml
- name: Veeem ONE v10 RTM Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: false
    vbr_setup: false
    vbr_license: false
    vbr_source_license: "/root/ansible/license.lic"
    vbr_source: "E:\\"
    vbr_update: false
    one_setup: true
    one_license: true
    one_source_license: "/root/ansible/license.lic"
    one_source: "D:\\"
    one_update: false
  roles:
    - veeam_setup
```

### Veeam ONE Free Edition Setup

```yaml
- name: Veeem ONE v10 RTM Free Edition Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_setup: false
    vbr_update: false
    one_setup: true
    one_update: false
  roles:
    - veeam_setup
```

## License

GNU Lesser General Public License v3.0

## Author Information

Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)

MY CLOUD-(R)EVOLUTION [mycloudrevolution.com](http://mycloudrevolution.com/)