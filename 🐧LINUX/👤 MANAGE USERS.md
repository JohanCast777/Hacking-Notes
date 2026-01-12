==LIST USERS==

ALL USERS
```
compgen -u
```

ORIGINAL USERS
```
awk -F: '$3 >= 1000 {print $1, $3}' /etc/passwd
```

![[Pasted image 20251229235753.png|1000]]


==SWITCH INTO USERS==
```
su alice
```

Execute a command as a different user
```
su -c "ls /home/alice" alice
```

==CREATE USERS==
```
sudo useradd alice
```

```
sudo passwd alice
```

| Option          | Meaning                                  | Simple example                               |
| --------------- | ---------------------------------------- | -------------------------------------------- |
| `-m`            | Create the user’s home directory.        | `sudo useradd -m alice`                      |
| `-M`            | Do **not** create a home directory.      | `sudo useradd -M alice`                      |
| `-d /path/home` | Use a custom home directory path.        | `sudo useradd -m -d /opt/alice alice`        |
| `-s /bin/bash`  | Set the user’s login shell.              | `sudo useradd -m -s /bin/bash alice`         |
| `-G g1,g2`      | Add user to extra supplementary groups.  | `sudo useradd -m -G sudo,developers alice`   |
| `-u 1050`       | Set a specific numeric UID for the user. | `sudo useradd -m -u 1050 alice`              |
| `-r`            | Create a system account (for services).  | `sudo useradd -r -s /usr/sbin/nologin nginx` |

==DELETE USERS==

Delete user and check if port in process
```
sudo userdel alice
```

Check the current services related with the port
```
ps -p 36502 -o pid,user,cmd
```

Stop process 
```
sudo kill -9 36502
```

Delete it
```
sudo userdel alice
```

==LIST GROUPS==
```
cat /etc/group
```

Check if it was created successfully 
```
getent group group1
```

==CREATE A GROUP==

```
sudo addgroup group1
```

```
sudo addgroup --gid 1500 group1
```

```
sudo addgroup group3 --shell /bin/sh
```

```
sudo addgroup --system group4 
```


==DELETE A GROUP==

```
sudo delgroup group1
```

==EDIT USER==

Change user name
```
sudo usermod -l newname oldname
```

Change the user’s numeric UID.
```
sudo usermod -o -u 0 fakeuser
```

Assign user to a group
```
sudo usermod -aG developers alice
```

Change one group to another
```
sudo usermod -g newgroup username
```

Lock an user

```
sudo usermod --lock username
```

