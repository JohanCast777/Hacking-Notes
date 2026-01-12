

==Saves ways==


- All output  (`-oA`) =  `all`
- Normal output (`-oN`) =  `.nmap`
- Grepable output (`-oG`) = `.gnmap`
- XML output (`-oX`) = `.xml` 


==Files created==

| File   | Content Description                                                                                                                          |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| .nmap  | Human-readable summary: target IP/hostname, open ports, discovered services, scan time.                                                      |
| .gnmap | One line per host: host status, open ports (comma-separated), port states, service banners, suitable for command-line processing.            |
| .xml   | Fully structured scan report: hosts, port states, scripts, metadata, time stamps—intended for XML parsers or tools likexsltprocorNmapViewer. |
==.XML==

sudo apt install xsltproc

xsltproc target.xml -o target.html

open target.html

![[Pasted image 20251015224334.png]]