# Ansible Role: Backup

Run daily backups on Debian and Ubuntu servers.

## Dependencies

Installed PHP CLI and drush (global)

## Example Playbook

    - hosts: server-name
      vars:
        backup_sets:
          - name: etc
            src: /etc
      roles:
        - AlphaNodes.backup

## License

GPL Version 3

## Author Information

This role was created in 2017 by [AlphaNodes](https://alphanodes.com/).
