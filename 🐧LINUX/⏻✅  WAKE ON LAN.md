
list all the interfaces
```
ip link
```

Check if supports Wol
```
sudo ethtool {Interface name}
```

Here we confirm support wol

![[Pasted image 20260116234055.png]]


Install the app in android wol

![[Pasted image 20260117000018.png]]

Set this configuration

![[Pasted image 20260117000040.png|400]]

Now let's see if it works
```
sudo poweroff
```

Alternative with another pc instead of phone
```
sudo apt install wakeonlan -y
```

```
wakeonlan 00:e0:4c:36:1b:af
```

