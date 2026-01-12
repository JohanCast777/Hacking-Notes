

![[Pasted image 20260102184322.png]]

==START SERVICES==

Install tools for use ssh
```
sudo apt install openssh-server -y
```

Start ssh service
```shell-session
systemctl start ssh
```

Check the status
```shell-session
systemctl status ssh
```

Say system active when startup
```shell-session
systemctl enable ssh
```

View the logs for troubleshooting
```shell-session
journalctl -u ssh.service --no-pager
```

==CHECK SERVICES==

Confirm service  running
```shell-session
ps -aux | grep ssh
```

```shell-session
systemctl list-units --type=service
```

```
HTOP
```

Check the ID
```
pgrep firefox
```

==SERVICES IN THE BACKGROUND==

Suspends the command
```
Ctl + Z
```

Show the jobs started for the terminal
```
jobs
```
Make run a service in the background
```
bg [number of the process]
```

Stop background, or only using the 2 commands bring it to the foreground 
```
fg, [number of the process], Ctl + Z
```

Start a process in the bg,  just using "&"
```
ping 8.8.8.8 &
```


==KILL SERVICES==

Check the is of the service
```
pgrep firefox
```

Kill service with the id
```
kill 1808
```

Kill definitely 
```
Kill -9 1808
```

Kill with name
```
pKill -9 ping
```

Help
```
kill -l
```

