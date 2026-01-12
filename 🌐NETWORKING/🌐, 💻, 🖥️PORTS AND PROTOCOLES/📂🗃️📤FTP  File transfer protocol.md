==Install the script== sudo apt install ftp

==Help in FTP== ftp -?

==Get into the machine==  ftp (ip)

==User by default== anonymous

==Commands after stay inside== cd, ls, get, help.

==RFC= Framework File transfer== [RFC959](http://www.faqs.org/rfcs/rfc959.html)



-----
# THEORY

FTP 2 channels
No Encryption
SFTP and FTPS(local ntwk)



![[Pasted image 20251110204049.png]]


![[Pasted image 20251110204307.png]]



![[Pasted image 20251110203351.png |500]]



==ROLES==

1. **Control Channel**: Command center
    
2. **Data Channel**: Just transport data


==TYPES OF TRANSMITION==

|Mode|Port Chosen By|Client Action|Server Action|
|---|---|---|---|
|Active|Client|Listens on a random port|Connects to client's port|
|Passive|Server|Connects to server's specified port|Listens on a random port (range)|

|Mode|When to Use|
|---|---|
|Active|Trusted networks, no strict client firewall|
|Passive|Client behind firewall/NAT, restrictive networks|

==KNOW PORT IN PASIVE MODE==

```shell-session
┌─[eu-academy-1]─[10.10.14.21]─[htb-ac-594497@htb-5mix2gkv1a]─[~]
└──╼ [★]$ nc 10.129.233.197 21
  
220 Microsoft FTP Service
USER anonymous^M
331 Anonymous access allowed, send identity (e-mail name) as password.
PASS anything^M
230 User logged in.
PASV^M
227 Entering Passive Mode (10,129,233,197,194,40).
```

==`194` * `256` + `40` = `49704`==


==COMMANDS==
**RETR**

==CONNECT WITH NMAP==



