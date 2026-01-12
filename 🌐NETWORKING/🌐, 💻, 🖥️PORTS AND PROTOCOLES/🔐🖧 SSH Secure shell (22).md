
Secure way to control another computer's terminal

Install
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

Stops the ssh service
```
sudo systemctl disable --now ssh.socket
```
```
sudo systemctl stop ssh
```

Connect using ssh
```
ssh user@ip   (optional use -p 443) 
```

Documents to set rules 
```
/etc/ssh/sshd_config
```

In case the machine has firewall first check the status
```
sudo ufw status
```

unable the firewall
```
sudo ufw allow ssh
```
```
sudo ufw allow 22/tcp
```

enable firewall and deny access to ssh(port 22)
```
sudo ufw allow ssh
```
```
sudo ufw enable
```
```
sudo ufw delete allow 22/tcp
```
```
sudo ufw deny 22/tcp
```



How to check if we have a connection established, So if someone is connected to us?
```
who
```




## ADDITIONAL INFO, KEYS

| File name         | Type           | Purpose                                                    | Security notes                                                                             |
| ----------------- | -------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `id_rsa`          | Private key    | RSA private key for SSH authentication                     | Must stay secret; if leaked, attacker can log in as you on any trusted host                |
| `id_rsa.pub`      | Public key     | RSA public key you copy to servers (`authorized_keys`)     | Safe to share; only grants access when paired with your private key                        |
| `id_ed25519`      | Private key    | Ed25519 private key (modern, preferred)                    | Same risk as `id_rsa`; rotate immediately if you suspect compromise                        |
| `id_ed25519.pub`  | Public key     | Ed25519 public key                                         | Safe to share; used to set up key‑based logins                                             |
| `authorized_keys` | Access control | Lists public keys allowed to log in to _this_ user account | Any key in here can log in as this user; remove unknown or old keys                        |
| `known_hosts`     | Host database  | Remembers server host keys you have connected to before    | Used to detect host key changes (possible MITM); delete entry if host changed legitimately |
| `config`          | Client config  | Per‑user SSH client options (hosts, ports, keys, etc.)     | Can reveal hostnames, usernames, custom ports; keep readable only by you                   |
| `id_ecdsa`        | Private key    | ECDSA private key (older elliptic‑curve type)              | Same rules as other private keys; avoid using on new setups if possible                    |
| `id_ecdsa.pub`    | Public key     | ECDSA public key                                           | Same as other `.pub` keys; safe to share for access setup                                  |

Check the keys created
```
ll ~/.ssh
```

Create a new key
```
ssh-keygen -t ed25519 -C "Johan-test"
```

Remove
```
rm ~/.ssh/id*
```

Associate key with server
```
ssh-copy-id -i ~/.ssh/test1.pub lubuntu@192.168.1.7
```

Connect to the server (Here first ask for the key pass, and then for the server pass)
```
ssh -i ~/.ssh/test1 lubuntu@192.168.1.7
```

