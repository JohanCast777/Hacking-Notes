
==WHICH==

==FIND==

| **Option**            | **Description**                                                                                                                                                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-type f`             | Hereby, we define the type of the searched object. In this case, '`f`' stands for '`file`'.                                                                                                                                                                                    |
| `-name *.conf`        | With '`-name`', we indicate the name of the file we are looking for. The asterisk (`*`) stands for 'all' files with the '`.conf`' extension.                                                                                                                                   |
| `-user root`          | This option filters all files whose owner is the root user.                                                                                                                                                                                                                    |
| `-size +20k`          | We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB.                                                                                                                                                           |
| `-newermt 2020-03-03` | With this option, we set the date. Only files newer than the specified date will be presented.                                                                                                                                                                                 |
| `-exec ls -al {} \;`  | This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection. |
| `2>/dev/null`         | This is a `STDERR` redirection to the '`null device`', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must `not` be an option of the 'find' command.                                  |


| Option            | What it does / filters                                   | Practical example                                                                                                                                   |
| ----------------- | -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-name`           | Match file name (case‑sensitive)                         | `find . -name "*.log"` [ionos](https://www.ionos.com/digitalguide/server/configuration/linux-find-command/)​                                        |
| `-iname`          | Match file name, case‑insensitive                        | `find . -iname "readme*"` [quickref](https://quickref.me/find.html)​                                                                                |
| `-type f`         | Only **regular files**                                   | `find . -type f -name "*.txt"` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                           |
| `-type d`         | Only **directories**                                     | `find . -type d -name ".git"` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                            |
| `-type l`         | Only **symbolic links**                                  | `find . -type l -name "Pictures"` [man7+1](https://man7.org/linux/man-pages/man1/find.1.html)​                                                      |
| `-type s`         | Only **sockets**                                         | `find /var -type s` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                                      |
| `-type p`         | Only **FIFOs** (named pipes)                             | `find . -type p` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                                         |
| `-type b`         | **Block** devices                                        | `find /dev -type b` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                                      |
| `-type c`         | **Character** devices                                    | `find /dev -type c` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                                      |
| `-size`           | Filter by size (`+` bigger, `-` smaller, units `k/M/G`)  | `find /var -type f -size +100M` [phoenixnap](https://phoenixnap.com/kb/guide-linux-find-command)​                                                   |
| `-mtime`          | Days since last modification                             | `find . -type f -mtime -7` [ionos+1](https://www.ionos.com/digitalguide/server/configuration/linux-find-command/)​                                  |
| `-mmin`           | Minutes since last modification                          | `find . -mmin -60` [stackoverflow](https://stackoverflow.com/questions/25599094/explaining-the-find-mtime-command)​                                 |
| `-user`           | Files owned by a given user                              | `find /home -user ubuntu` [ionos](https://www.ionos.com/digitalguide/server/configuration/linux-find-command/)​                                     |
| `-group`          | Files belonging to a given group                         | `find /home -group www-data` [quickref](https://quickref.me/find.html)​                                                                             |
| `-perm`           | Exact permissions                                        | `find / -type f -perm 0777` [tecmint](https://www.tecmint.com/35-practical-examples-of-linux-find-command/)​                                        |
| `-empty`          | Empty files or directories                               | `find . -empty` [ionos](https://www.ionos.com/digitalguide/server/configuration/linux-find-command/)​                                               |
| `-maxdepth`       | Maximum directory depth                                  | `find . -maxdepth 1 -type f` [quickref](https://quickref.me/find.html)​                                                                             |
| `-mindepth`       | Minimum directory depth (skip upper levels)              | `find . -mindepth 2 -name "*.txt"` [quickref](https://quickref.me/find.html)​                                                                       |
| `!` / `-not`      | Negate the next test                                     | `find . -type f ! -name "*.txt"` [quickref](https://quickref.me/find.html)​                                                                         |
| `-o` / `-a`       | Logical OR / AND between tests                           | `find . \( -name "*.sh" -o -name "*.py" \)` [quickref](https://quickref.me/find.html)​                                                              |
| `-path`           | Match against the **full path**                          | `find . -path "./src/**/*.py"` [stackoverflow+1](https://stackoverflow.com/questions/1489277/how-to-use-prune-option-of-find-in-sh)​                |
| `-prune`          | Do not descend into matching directories                 | `find . -path "./.git" -prune -o -type f -print` [theunixschool+1](https://www.theunixschool.com/2012/07/find-command-15-examples-to-exclude.html)​ |
| `-exec cmd {} \;` | Run `cmd` once **per result**                            | `find . -type f -name "*.log" -exec rm {} \;` [phoenixnap+1](https://phoenixnap.com/kb/guide-linux-find-command)​                                   |
| `-exec cmd {} +`  | Run `cmd` with **many results at once** (more efficient) | `find . -type f -name "*.log" -exec gzip {} +` [quickref](https://quickref.me/find.html)​                                                           |
| `-ok cmd {} \;`   | Like `-exec` but asks for confirmation                   | `find . -type f -ok rm {} \;` [phoenixnap](https://phoenixnap.com/kb/guide-linux-find-command)​                                                     |
| `-print`          | Print the path (basic default behavior)                  | `find . -type f -print` [man7](https://man7.org/linux/man-pages/man1/find.1.html)​                                                                  |
| `-print0`         | Print paths separated by `\0` (safe for `xargs -0`)      | `find . -print0 \| xargs -0 rm` [quickref](https://quickref.me/find.html)​                                                                          |
| `-delete`         | Directly delete the matched files                        | `find . -type f -name "*.tmp" -delete` [phoenixnap+1](https://phoenixnap.com/kb/guide-linux-find-command)​                                          |
| > test.txt        | Save output in a file                                    | find /etc/ -name shadow 2>/dev/null > test.txt                                                                                                      |

==LOCATE==

**UPDATE DATABASE CONTAIN INFO**  

```shell-session
sudo updatedb
```
**EXAMPLE**

```shell-session
locate *.conf
```

**COUNT HOW MAY TIMES APPEARS A FILE**

```shell-session
locate "*bak" | wc -l
```

**USE WITH GREP**

```shell-session
find /etc/ -name *.conf 2>/dev/null | grep systemd
```

**APPS INSTALLED**

```shell-session
dpkg --get-selections | grep -w "install"
```

**HOW MANY SERVICES ARE LISTENING**

```shell-session
netstat -ln4 | grep LISTEN | grep -v 127 | wc -l
```
