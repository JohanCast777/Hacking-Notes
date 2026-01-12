Store files in remote system

==SERVER==

Install protocol
```shell-session
sudo apt install nfs-kernel-server -y
```

Check the status

```shell-session
systemctl status nfs-kernel-server
```

## File to set it up

```
/etc/exports
```

| **Permissions**  | **Description**                                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `rw`             | Gives users and systems read and write permissions to the shared directory.                                                                                |
| `ro`             | Gives users and systems read-only access to the shared directory.                                                                                          |
| `no_root_squash` | Prevents the root user on the client from being restricted to the rights of a normal user.                                                                 |
| `root_squash`    | Restricts the rights of the root user on the client to the rights of a normal user.                                                                        |
| `sync`           | Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system.                               |
| `async`          | Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed. |
| no_subtree_check | Just have access to the firectory specified, not the subtree files.                                                                                        |

Change the name of the original name
```
sudo mv /etc/exports /etc/exports.org
```

Create another file replacing the previous name
```
sudo nano /etc/exports
```

Add this to the file (IP of the client)
```
/home/ubuntu/Documents/work/workhacking/exports/backup 192.168.1.55(rw,no_subtree_check)

```


Restart the protocol

```
systemctl restart  nfs-kernel-server
```


==CLIENT==

```
sudo apt install nfs-common
```

Test connectivity with the server

```
showmount --exports 192.168.1.4
```

 Create a directory to sav the shared files
```
sudo mkdir /mnt/nfs
```

```
sudo mkdir /mnt/nfs/backup
```

```
sudo mkdir /mnt/nfs/documents
```

Mount the directory
```
sudo mount 192.168.1.4:/home/ubuntu/Documents/work/workhacking/exports/backup /mnt/nfs/backup
```

Check the mount list of the files
```
df -h
```
## UNMOUNT

==CLIENT==

```
sudo umount  /mnt/nfs/backup
```

## AUTO FS

==CLIENT==

Remove the files previosly created
```
sudo rm -rf /mnt/nfs/backup
```

Install Autofs
```
sudo apt install autofs
```

Chedck out the status 
```
systemctl status autofs
```

Update this file to use the Autofs    ("Master file is the first file system reads when starts up")
```
sudo nano /etc/auto.master
```

Add to the files int he last part this

```
/mnt/nfs /etc/auto.nfs --ghost --timeout=60
```

 Go to edit the files with all the instructions
 ```
 nano /etc/auto.nfs
 ```

```
backup -fstype=nfs4,rw 192.168.1.4:/home/ubuntu/Documents/work/workhacking/exports/backup
```

Restar to see everything reflected 
```
sudo systemctl restart autofs  
```

Everything is mounted in this directory

```
/mnt/nfs
```

