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
ssh-copy-id -i ~/.ssh/test1.pub lubuntu@192.168.1.7(localhost if same pc)
```

Now we will create an script for automate the rsync backup. RSYNC_Backup.sh

```bash
#!/bin/bash

rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

Change the permissions of the file
```shell-session
chmod +x RSYNC_Backup.sh
```

Use #crontab to schedule the time that will works
```
crontab -e
```



## Duplicity (Encrypt backups) 🔴

Installation
```
sudo apt install duplicity
```

Make a backup
```
duplicity /home/ubuntu/Documents \
file:///home/ubuntu/Documents/duplicity-backups
```

Restore the backup
```
duplicity restore \ file:///home/ubuntu/Documents/duplicity-backups \ /home/ubuntu/Documents/restore-docs
```

Encrypt it
```
export PASSPHRASE="MyStrongPassphrase"
```

```
duplicity /home/ubuntu/Documents \   file:///home/ubuntu/Documents/duplicity-backups 
```

```
unset PASSPHRASE
```

##  Deja Dup (Encrypt backups, everyone can operates it) 🟢

Installation
```
sudo apt install deja-dup -y
```

check if we have duplicty also installed
```
duplicity --version
```

Start Deja dup
```
deja-dup
```


After open it up, check the preferences and choose the storage location, and also schedule it
![[Pasted image 20260117005354.png|400]]


This is the main interface, click on "Create your first backup"
![[Pasted image 20260117005154.png|500]]

Slect the folder to backup and the ones to ignore
![[Pasted image 20260117143235.png|500]]


Set a password
![[Pasted image 20260117143629.png]]

Now the folder would be backed up, and here is how it looks like
![[Pasted image 20260117143911.png]]