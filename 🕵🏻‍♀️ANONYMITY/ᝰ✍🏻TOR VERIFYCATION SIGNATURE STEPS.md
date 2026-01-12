**WINDOWS**

Download this documents 

![[Pasted image 20250906165651.png]]

Put the sollowing commands

cd C:/Users/casta/Downloads/Tor

gpg --auto-key-locate nodefault,wkd --locate-keys torbrowser@torproject.org

gpg --output ./tor.keyring --export 0xEF6E286DDA85EA2A4BA7DE684E2C6E8793298290

gpg --verify "tor-browser-windows-x86_64-portable-14.5.6.exe.asc" "tor-browser-windows-x86_64-portable-14.5.6.exe"

![[Pasted image 20250906170439.png]]
	

**LINUX**

![[Pasted image 20250906190837.png]]