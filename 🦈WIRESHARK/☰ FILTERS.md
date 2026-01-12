
IP SOURCE= ip.src == 192.168.1.4
IP DESTINATION= ip.dst == 192.168.1.4

MAC SOURCE = eth.src == fe80::7b3:e701:a161:1cc5%14
MAC  DESTINATION= eth.dst == fe80::7b3:e701:a161:1cc5%14

HTTP= ip.addr == 192.168.1.4 && http
HTTPS= ip.addr == 192.168.1.4 && tcp.port == 443

TYPE OF FLAGS FILTER=tcp.flags.syn == 1

EXCLUDE SOME PROTOCOLES= not (arp or ipv6 or ssdp)

FILTER BY PORT= tcp.port == 80 or tcp.port == 443 or tcp.port == 8080

SEARCH BY TEXT NON ENCRIPTED= frame contains http