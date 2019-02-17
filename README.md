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

```
backup_dir: /srv/backups
```

Directory for backups. Make sure there is enough disk space at this disk partition.


```
backup_dir_mode: 0755
```

Directory permission for `backup_dir`


```
backup_dir_owner: root
```

Directory owner for `backup_dir`


```
backup_dir_group: root
```

Directory group for `backup_dir`


```
backup_max_days: 7
```

Amount of days for daily backup sets. This means only `backup_max_days` set (days) are stored. Older sets are deleted automatically. Values has to be => 1.


```
backup_max_weeks: 1
```

Amount of weeks for weekly backup sets. This means only `backup_max_weeks` set (weeks) are stored. Older sets are deleted automatically. Values has to be => 1. The weekly backup is created every first day of the week. At this day only this backup is created (and no daily backup - because this would be duplicate).


```
backup_max_months: 1
```

Amount of weeks for weekly backup sets. This means only `backup_max_months` set (months) are stored. Older sets are deleted automatically. Values has to be => 1. The monthly backup is created every first day of the month. At this day only this backup is created (and no daily or weekly backup - because this would be duplicate).


```
backup_remote_host: ''
```

Hostname to sync backups for `backup_remote_transfer` usage.

```
backup_remote_port: ''
```

Port to sync backups for `backup_remote_transfer` usage.


```
backup_remote_dir: ''
```

Remote directory of for `backup_remote_host` for `backup_remote_transfer` usage.

```
backup_remote_excludes:
  - '*.journal'
  - '.nfs*'
  - '*.tar'
```

These file are excluded of sync to remote host. This is only used if `backup_remote_transfer` is `rsync`.


```
backup_rsync_options: '-avz --delete'
```

rsync options for `backup_remote_transfer` with `rsync`.


```
backup_remote_transfer: rsync
```

Type of sync. Possible values are: rsync or lftp


```
backup_remote_user: ''
```

User for remote sync. This is only used  with `backup_remote_transfer` is lftp.


```
backup_remote_password: ''
```

Password for remote sync. This is only used  with `backup_remote_transfer` is lftp.


```
backup_db_dump_format: .sql.gz
```

Uncompressed SQL files (.sql) as well as bzip2 (.bz2), gzip (.gz) and xz. At the moment only used for mysql dumps.


```
backup_with_mysql: no
```

Run MySQL (MariaDB) backup dump.


```
backup_with_postgresql: no
```

Run PostgreSQL backup dump.


```
backup_mysql_db_excludes:
  - performance_schema
  - information_schema
  - sys
```

```
backup_mysql_single_transaction: yes
```

```
# backup_mysqldump_options: '--extended-insert=true --opt --single-transaction'
```

Custom mysql options (always sql.gz is used). If set native mysql_dump (without ansible) is used. Default this is not set.


```
backup_postgresqldump_options: "--no-owner -Fc"
```

PostgreSQL dump options.


```
backup_create_hashfiles: no
```

Create hash files of all backup sets.



```
backup_files_unsafe_writes: no
```

If `backup_files_unsafe_writes` is yes and changed files are found while creating tar files, no error are reported. tar runs with the additional options `--warning=no-file-removed --warning=no-file-changed --warning=no-file-ignored`.


```
backup_sets: []
  - name: etc
    src: /etc
  - name: jenkins
    src: /var/lib/jenkins
    unsafe_writes: yes
    excludes:
      - builds
      - workspace
```

Backup sets for file backup. `name` is used as backup file name. `src` is the directory of file, which should be back uped.


```
backup_one_per_day_limit: yes
```

Create only one backup set per day. Existing backup sets of same day will be removed.


```
#sync_master: anything
```

If sync_master is defined, backup will be skipped. You can use it for replication environments.


```
backup_skip_sync_clients: yes
```

If sync_master is defined, this means it is a sync_client.


```
backup_pre_commands: []
```

List of commands, which should be run before backup dump.



```
backup_post_commands: []
```

List of commands, which runs after backup dump has been created.



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
