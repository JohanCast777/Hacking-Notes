## Rsync (Backups)🟡

```
sudo apt install rsync -y
```

Backup our machine
```
rsync -av /home/ubuntu/Documents/work/workhacking/backupstest/original/ \
/home/ubuntu/Documents/work/workhacking/backupstest/backup/
```
Backup in other server
```shell-session
rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```
## Duplicity (Encrypt backups) 🔴

##  Deja Dup (Encrypt backups, everyone can operates it) 🟢

