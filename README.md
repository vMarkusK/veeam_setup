veeam_setup
=========

An Ansible Role that installs and updates [Veeam](https://www.veeam.com) components (Veeam Backup & Replication / Veeam ONE) on Windows.

Requirements
------------

none

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
---
# defaults file for veeam_setup

## Choose Setup
vbr_setup: true
vbr_update: true
one_setup: false

## VBR Parameters
vbr_source: "D:\\"
vbr_update_file: "veeam_backup_9.5.4.2866.update4b_setup.exe"
vbr_update_id: "Veeam VBR Update 4b"
sql_username: "svc_sql"
sql_userpassword: "ChangeM3!"
sql_sapassword: "ChangeM3!"
```

Dependencies
------------

none

Example Playbook
----------------

```yaml
- name: VBR Community Edition Setup
  hosts: veeam
  gather_facts: no
  roles:
    - veeam_setup
```

License
-------

GNU Lesser General Public License v3.0

Author Information
------------------

Markus Kraus [@vMarkus_K](https://twitter.com/vMarkus_K)
MY CLOUD-(R)EVOLUTION [mycloudrevolution.com](http://mycloudrevolution.com/)