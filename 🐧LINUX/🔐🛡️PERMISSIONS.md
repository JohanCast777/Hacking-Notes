 
![[Pasted image 20251228122413.png|500]]

![[Pasted image 20251223174254.png]]

|Character|Meaning|Description|
|---|---|---|
|`-`|Regular file|Normal file containing data, text, binaries, etc.|
|`d`|Directory|Folder that can contain files and other directories.|
|`l`|Symbolic link|Reference (shortcut) pointing to another file or directory.|
|`b`|Block device|Hardware device accessed in blocks (e.g., disks).|
|`c`|Character device|Device accessed as a stream of characters (e.g., terminals).|
|`s`|Socket|Endpoint for inter-process/network communication.|
|`p`|FIFO/Named pipe|Special file for one-way inter-process communication.|

==CHANGE THE OWNER==

![[Pasted image 20251228185145.png]]

![[Pasted image 20251228185543.png]]

==CHANGE PERMISSIONS==

```shell-session
chmod a+r shell && ls -l shell
```
`u` = user
 `g` = group
 `o` = others 
 `a` = all
 
![[Pasted image 20251228230546.png]]

==CREATE SYMBOLIC LINKS==
ln -s test test2

| Feature    | Applies to  | Simple meaning                                                                                                      | How it shows in `ls -l`                                                                                             | Typical use / effect                                                                                                                                    | Example command & result (conceptual)                                                                                                                                               |
| ---------- | ----------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SUID**   | Files       | Run the program **as the file’s owner**. [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​           | User execute becomes `s`: `-rwsr-xr-x` [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​             | Let normal users run a program with the owner’s (often root’s) powers. [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​                 | `chmod u+s /usr/bin/myprog` → Users run `myprog` and it executes with the owner’s UID (e.g. root). [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​                 |
| **SGID**   | Files       | Run the program **with the file’s group**. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​ | Group execute becomes `s`: `-rwxr-sr-x` [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​            | Shared tools that need a specific group’s access. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​                              | `chmod g+s /usr/local/bin/teamtool` → Users run it with the group of `teamtool`. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​                           |
| **SGID**   | Directories | New files inherit the **directory group**. [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​         | Directory with `s` in group execute: `drwxr-sr-x` [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​  | Shared project folder: all files get same group, easier collaboration. [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​                 | `chmod g+s /srv/projects` → Files created in `/srv/projects` get group `projects`, not user’s default group. [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​       |
| **Sticky** | Directories | Users can delete **only their own files**. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​ | `t` in others execute: `drwxrwxrwt` (like `/tmp`). [redhat+1](https://www.redhat.com/en/blog/suid-sgid-sticky-bit)​ | Shared directories where everyone writes, but no one can delete others’ stuff. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​ | `chmod +t /shared` → Everyone can create files in `/shared`, but only the owner (or root) can delete them. [scaler+1](https://www.scaler.com/topics/special-permissions-in-linux/)​ |

==Sticky== Only owner and root can = Delete or Write

ADD
```
chmod +t test
```

```
chmod 1777 test
```

REMOVE
```
chmod 0777 test
```

```
chmod -t test
```


