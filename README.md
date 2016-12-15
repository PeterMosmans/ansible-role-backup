Ansible Role: backup
=========

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-backup.svg)](https://travis-ci.org/PeterMosmans/ansible-role-backup)

This role backs up databases and (web) directories from a server, and transfers the backup files to a local destination.

Requirements
------------

If you want to backup MySQL databases, then the server needs to have the Python library `mysql-python` installed.

Role Variables
--------------

Available variables are listed below, along with their default values. The defaults can be found in ```defaults/main.yml```.

**backup_directories**: A list of name / src pairs of directories that will be backed up. Each item contains the full source directory (src), and the corresponding backup name (name). Example:
```
- backup_directories:
  - name: mywebsite
    src: /var/www/html
```

**backup_location_local**: The directory name of the *local* destination, where the backup files will be transferred to. Defaults to `/tmp`. Note that a subdirectory will be created, with the value of the `inventory_hostname` variable.

**backup_location_remote**: The temporary location of the backup files on the *remote* server. Defaults to `/tmp/backup`

**backup_mysql_databases**: A list of MySQL databases that will be backed up. The corresponding backup file will be named `<name>.sql.gz`.


Dependencies
------------

None.

Example Playbook
----------------
```
- hosts: all
  become: yes
  become_method: sudo
  roles:
    - role: PeterMosmans.backup
  vars:
    - backup_mysql_databases:
      - mydatabase
    - backup_directories:
      - name: mywebsite
        src: /var/www/mywebsite
```

License
-------
GPLv3


Author Information
------------------
Created by Peter Mosmans. Feedback always welcome.
