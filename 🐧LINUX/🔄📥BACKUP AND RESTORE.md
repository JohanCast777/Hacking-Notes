## Rsync (Backups)🟡

==Basic Commands==

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

This make a a backup, but don't delete any files 
```
rsync -avz --backup   --backup-dir=/home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld2   --delete   /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld1/   /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld2/
```

Restore backup directory
```
rsync -ac /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld2 /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld1
```

==Encryption==

Combine ssh to encrypt the files
```
rsync -avz -e ssh /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld1  /home/ubuntu/Documents/work/workhacking/backupstest/secondtest/fld2
```

==Auto-Synchronization==

#Create_new_key
```shell-session
ssh-keygen -t rsa -b 2048
```

Associate with the specific location
```shell-session
ssh-copy-id -i ~/.ssh/test1.pub lubuntu@192.168.1.7
```

Now we will create the an script to create the rsync backup.
## Duplicity (Encrypt backups) 🔴



##  Deja Dup (Encrypt backups, everyone can operates it) 🟢

