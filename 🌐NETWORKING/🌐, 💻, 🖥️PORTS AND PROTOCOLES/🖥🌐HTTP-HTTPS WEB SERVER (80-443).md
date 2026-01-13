
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

## CURL and WGET

Check the html
```
curl http://localhost
```
```
wget http://localhost
```


|Task|CURL|WGET|
|---|---|---|
|**Basic download**|`curl URL`|`wget URL`|
|**Save as file**|`-o file.txt`|`-O file.txt`|
|**POST data**|`-d "data"`|`--post-data="data"`|
|**Custom header**|`-H "Header"`|`--header="Header"`|
|**Authentication**|`-u user:pass`|`--user=user --password=pass`|
|**Upload file**|`-F "file=@file.txt"`|❌ Not supported|
|**Mirror website**|❌ Limited|`--mirror` ✅|
|**HTTP method**|`-X POST`|Limited|
|**Timeout**|`-m 10`|`--timeout=10`|
|**Retries**|`--retry 5`|`--tries=5`|
|**Cookies**|`-b -c`|`--load-cookies --save-cookies`|
|**Verbose**|`-v`|`-v`|
|**Follow redirects**|`-L`|Default ✅|
|**Bandwidth limit**|`--limit-rate`|`--limit-rate`|
|**Range request**|`-r 0-99`|❌ Not supported|

## NMP

Install
```
npm install -g http-server
```

Connect  the server 
```
http-server -p 8080
```

## PHP

```
php -S localhost:8080
```

