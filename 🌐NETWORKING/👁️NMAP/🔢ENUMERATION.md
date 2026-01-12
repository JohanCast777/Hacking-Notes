Important to search the accurate exploit
## 🔎Version

==Version Detection==
```shell-session
sudo nmap 10.129.2.28 -p- -sV
```



## 🚩BANNER
Automatic first response from the target

==Capture transmitted between two hosts==
```shell-session
sudo tcpdump -i eth0 host 10.10.14.2 and 10.129.2.28
```

==Establish communication with one specific port ==
```shell-session
nc -nv 10.129.2.28 25
```

```shell-session
ncat -nv --source-port 53 10.129.2.28 50000
```


