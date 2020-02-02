# veeam_setup

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

## Requirements

none

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
---
# defaults file for veeam_setup

## Choose Setup
vbr_download: false
vbr_setup: false
vbr_update: false
one_setup: false

## VBR Parameters
one_source: "E:\\"
one_username: "svc_one"
one_userpassword: "ChangeM3!"
one_update_file: "VeeamONE_9.5.4.4587_Update#4a.exe"
one_update_id: "Veeam ONE Update 4a"
vbr_url: "https://download2.veeam.com/VeeamBackup&Replication_9.5.4.2615.Update4.iso"
vbr_checksum: "8a594cec74059f9929ea765ac5e70a49da6fc93803b567cbb9d74fbb1a49a6cc"
vbr_destination: "C:\\install\\"
vbr_destination_file: "vbr.iso"
vbr_source: "D:\\"
vbr_update_file: "veeam_backup_9.5.4.2866.update4b_setup.exe"
vbr_update_id: "Veeam VBR Update 4b"
sql_username: "svc_sql"
sql_userpassword: "ChangeM3!"
sql_sapassword: "ChangeM3!"
```

## Dependencies

none

## Example Playbook

### Veeam Backup & Replication Setup with local Download

```yaml
- name: Veeam Backup & Replication v10 Community Edition Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: true
    vbr_setup: true
    vbr_update: false
    one_setup: false
    one_update: false
  roles:
    - veeam_setup
```

### Veeam Backup & Replication Setup without local Download

```yaml
- name: Veeam Backup & Replication v10 Community Edition Setup
  hosts: veeam
  gather_facts: no
  vars:
    vbr_download: false
    vbr_setup: true
    vbr_update: false
    one_setup: false
    one_update: false
  roles:
    - veeam_setup
```

### Veeam ONE Setup

```yaml
- name: Veeem ONE v10 Free Edition Setup
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