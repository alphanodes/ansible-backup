# Ansible Role: Backup

Run daily backups on Debian and Ubuntu servers.

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-alphanodes.backup-660198.svg)](https://galaxy.ansible.com/AlphaNodes/backup)
[![Build Status](https://travis-ci.org/AlphaNodes/ansible-backup.svg?branch=master)](https://travis-ci.org/AlphaNodes/ansible-backup)

## Dependencies

Installed PHP CLI and drush (global)

## Installation

### Ansible 2+

Using ansible galaxy cli:

```bash
ansible-galaxy install alphanodes.backup
```

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
