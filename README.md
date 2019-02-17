# Ansible Role: Backup

Run daily, weekly and monthly backups for files, MySQL databases and PostgreSQL databases on Debian and Ubuntu servers.

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-alphanodes.backup-660198.svg)](https://galaxy.ansible.com/AlphaNodes/backup)
[![Build Status](https://travis-ci.org/AlphaNodes/ansible-backup.svg?branch=master)](https://travis-ci.org/AlphaNodes/ansible-backup)

## Dependencies

  none

## Installation

### Ansible 2+

Using ansible galaxy cli:

```bash
ansible-galaxy install alphanodes.backup
```

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):


## Example Playbook

```yaml
- hosts: server-name
  vars:
    backup_sets:
      - name: etc
        src: /etc
  roles:
    - AlphaNodes.backup
```

## License

GPL Version 3

## Author Information

This role was created in 2018 by [AlphaNodes](https://alphanodes.com/).
