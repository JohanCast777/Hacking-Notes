
Sharing files

==Install the script== sudo apt-get install smbclient

==List all the hosts inside== smbclient -L 10.129.28.224

==Try to access every host== smbclient \\\\10.129.28.224\\ADMIN$

==Commands after stay inside== cd, ls, get, help


