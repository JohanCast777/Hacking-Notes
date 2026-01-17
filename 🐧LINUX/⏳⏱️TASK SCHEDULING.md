
![[Pasted image 20260108133025.png|500]]

```shell-session
sudo mkdir /etc/systemd/system/mytimer.timer.d
```

When it will runs
```
sudo vim /etc/systemd/system/mytimer.timer
```

```txt
[Unit]
Description=My Timer

[Timer]
OnBootSec=3min
OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

What to run
```shell-session
sudo vim /etc/systemd/system/mytimer.service
```

```txt
[Unit]
Description=My Service

[Service]
ExecStart=/full/path/to/my/script.sh  [Here is the script path]

[Install]
WantedBy=multi-user.target
```


*Now this will read the files*

Ask folder systemd read the files
```
sudo systemctl daemon-reload
```

Start the timer now
```
sudo systemctl start mytimer.timer
```

Start it automatically on boot
```
sudo systemctl enable mytimer.timer
```

Reboot system to try



### Additional example with apps

Create a folder to save all the process will run
```
mkdir -p ~/.config/systemd/user
```

Create the What to run
```
sudo vim ~/.config/systemd/user/autostart-apps.service
```

```
[Unit]
Description=Start my GUI apps on login
After=graphical-session.target

[Service]
Type=simple
ExecStart= [path with file with the .sh]

[Install]
WantedBy=default.target

```

The file with .sh should have= 

```
#!/usr/bin/env bash

# start Firefox and VS Code in background
firefox & 
code &
```

Change permissions file
```
chmod +x /home/ubuntu/.local/bin/autostart-apps.sh
```

Enable it
```
systemctl --user daemon-reload 
systemctl --user enable autostart-apps.service 
systemctl --user start autostart-apps.service   # test now
```

--------

### Additional example with apps

This file executes yes or yes this when system starts  
```
mkdir -p ~/.config/autostart

cat > ~/.config/autostart/autostart-apps.desktop << 'EOF'
[Desktop Entry]
Type=Application
Exec=/home/ubuntu/Documents/work/workhacking/openapps.sh
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name=Autostart Hacking Apps
EOF
```

## #Crontab

Main file
```
cat /etc/crontab
```

Check crontabs set
```
crontab -l
```

Choose the user we will use 
```
crontab -u
```

Create a new crontab
```
crontab -e
```

This is what that should contains
```
1 * * * * /bin/echo "This is a test" > /home/ubuntu/Documents/work/test
```


#### What task scheduling is for
- Automatic backups, syncs, database dumps, log rotation.- ​
- Cleaning temp files, updating caches, trimming SSDs, system maintenance tasks.
- Running monitoring scripts, reports, notifications, etc., at fixed times or “every N minutes / after boot / after a service is up”.
