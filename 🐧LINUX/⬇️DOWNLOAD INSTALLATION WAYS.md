
![[Pasted image 20260102132003.png]]


==APT==

INFO LOCATED IN THIS REPOSITORY
```
/etc/apt/sources.list.d
```

SEARCH IN THE CACHE

```shell-session
apt-cache search impacket
```

```shell-session
apt-cache show packet_name
```


LIST INSTALLED PACKAGES

```shell-session
apt list --installed
```

INSTRALL PACKAGE

```shell-session
sudo apt install impacket-scripts -y
```

==GIT==

```
git clone https://github.com/samratashok/nishang.git
```

==DPKG==


```shell-session
wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
```


```shell-session
sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb 
```


==UNINSTALL==

```
sudo apt remove cursor
```

```
sudo rm /usr/bin/cursor
```

