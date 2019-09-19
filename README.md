# veeam_setup

An Ansible Role to install and update [Veeam](https://www.veeam.com) components (Veeam Backup & Replication / Veeam ONE) on Windows.

## Requirements

none

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
---
# defaults file for veeam_setup

## Choose Setup
vbr_setup: false
vbr_update: false
one_setup: false

## VBR Parameters
one_source: "E:\\"
one_username: "svc_one"
one_userpassword: "ChangeM3!"
one_update_file: "VeeamONE_9.5.4.4587_Update#4a.exe" # Fix Name
one_update_id: "Veeam ONE Update 4a"
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

### Veeam Backup & Replication Setup

```yaml
- name: Veeam Backup & Replication Community Edition Setup
  hosts: veeam
  gather_facts: no
  vbr_setup: true
  vbr_update: true
  one_setup: false
  one_update: false
  roles:
    - veeam_setup
```

### Veeam ONE Setup

```yaml
- name: Veeem ONE Free Edition Setup
  hosts: veeam
  gather_facts: no
  vbr_setup: false
  vbr_update: false
  one_setup: true
  one_update: true
  roles:
    - veeam_setup
```

## License

GNU Lesser General Public License v3.0

## Author Information

Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)

MY CLOUD-(R)EVOLUTION [mycloudrevolution.com](http://mycloudrevolution.com/)