
==MORE==
==LESS==

==HEAD==
```shell-session
head /etc/passwd
```
==TAIL==

```shell-session
tail /etc/passwd
```

==SORT==

```shell-session
cat /etc/passwd | sort
```


==CUT==

```shell-session
cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1
```

==TR== Replace things

```shell-session
cat /etc/passwd | grep -v "false\|nologin" | tr ":" "="
```

==COLUMN==

```shell-session
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t
```

==GREP==

```shell-session
cat /etc/passwd | grep "/bin/bash"
```

```shell-session
cat /etc/passwd | grep -v "false\|nologin"
```

```shell-session
curl https://www.inlanefreight.com/ | grep -Po 'https://www\.inlanefreight\.com/[^"'\'']*' | sort -u | wc -l
```

**REGEX**

![[Pasted image 20251222232714.png]]


```shell-session
grep -E "(my|false)" /etc/passwd
```

```shell-session
grep -E "my" /etc/passwd | grep -E "false"
```

```shell-session
grep -Ev "#" /etc/ssh/sshd_config
```

```shell-session
grep -E "\bPermit\w*" /etc/ssh/sshd_config
```

```shell-session
grep -E "\w*Permit\b" /etc/ssh/sshd_config
```

```shell-session
grep -E "\bPermit\b" /etc/ssh/sshd_config
```

