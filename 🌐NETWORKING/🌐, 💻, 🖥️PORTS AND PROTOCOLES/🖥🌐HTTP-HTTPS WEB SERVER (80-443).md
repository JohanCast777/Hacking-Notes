
Install apache web server
```shell-session
sudo apt install apache2 -y
```

check the status
```
systemctl status apache2
```
Run apache server
```
python3 -m http.server
```

Other option if we want to choose an specific directory 
```shell-session
 python3 -m http.server --directory /home/cry0l1t3/target_files
```

File to set
```
/etc/apache2/apache2.conf
```

Click on the link to open the folder
![[Pasted image 20260112185953.png]]

