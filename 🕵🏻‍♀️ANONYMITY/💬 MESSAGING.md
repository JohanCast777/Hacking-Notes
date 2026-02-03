
## SESSION

*Decentralized, no phone number required. Uses onion routing by default to hide your IP. Messages routed through Oxen service nodes, not a central server. No metadata collection—Session doesn't know who you're talking to.s*

==Installation in the OS==

Follow all this commands one by one to install it
```
cd ~/Downloads
```
```
curl -s https://api.github.com/repos/oxen-io/session-desktop/releases/latest | grep browser_download_url | grep AppImage | cut -d '"' -f 4
```
```
wget https://github.com/oxen-io/session-desktop/releases/download/v1.14.3/session-desktop-linux-x86_64-1.14.3.AppImage
```
```
chmod +x session-desktop-linux-x86_64-1.14.3.AppImage
```
```
sudo ./session-desktop-linux-x86_64-1.14.3.AppImage --no-sandbox
```


==Installation in a smartphone==

Install the app with this logo
![[Pasted image 20260203161543.png|200]]



## BRIAR
*Tor-native, works offline via Bluetooth mesh, best for activists in restricted areas*

==Installation in the OS==





==Installation in a smartphone==

Install the app with this logo
![[Pasted image 20260203162602.png]]

## SIGNAL
*Most user-friendly, military-grade encryption, requires phone number but no metadata tracking*

==Installation in the OS==



==Installation in a smartphone==

Install the app with this logo
![[Pasted image 20260203163505.png]]

## RICOCHET
*Pure Tor messenger, runs as .onion hidden service, zero metadata*

==Installation in the OS==


This can not be install in smartphone
![[Pasted image 20260203165041.png]]

## SIMPLEX CHAT
*No usernames/IDs, invitation-link based, decentralized*

==Installation in the OS==


==Installation in a smartphone==

Install the app with this logo
![[Pasted image 20260203165344.png]]


| App          | Anonymity | Tor-Native | Phone Required | Decentralized | Offline |
| ------------ | --------- | ---------- | -------------- | ------------- | ------- |
| **Session**  | ⭐⭐⭐⭐⭐     | Built-in   | No             | ✅             | ✅       |
| **Briar**    | ⭐⭐⭐⭐⭐     | Built-in   | No             | ✅             | ✅       |
| **Ricochet** | ⭐⭐⭐⭐⭐     | Native     | No             | ✅             | Limited |
| **Signal**   | ⭐⭐⭐       | Optional   | Yes            | ❌             | ❌       |
| **SimpleX**  | ⭐⭐⭐⭐      | Optional   | No             | ✅             | ❌       |

| App              | Android | iOS   | Desktop               |
| ---------------- | ------- | ----- | --------------------- |
| **Briar**        | ✅ Yes   | ❌ No  | ✅ Yes                 |
| **Signal**       | ✅ Yes   | ✅ Yes | ✅ Yes                 |
| **Ricochet**     | ❌ No    | ❌ No  | ✅ Yes (desktop only)  |
| **SimpleX Chat** | ✅ Yes   | ✅ Yes | ✅ Yes                 |
| **Tails OS**     | ❌ No    | ❌ No  | ✅ Yes (live USB only) |