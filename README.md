# youtubeUnblock on TP-Link Archer AX10 (AX1500)

## Get telnet root

https://github.com/gmaxus/TP-Link-Archer-AX1500-telnet-root

### Telnet to router
```text
telnet 192.168.0.1
```

### Iptables configuration
```text
iptables -t mangle -N YOUTUBEUNBLOCK
iptables -t mangle -A YOUTUBEUNBLOCK -p tcp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
iptables -t mangle -A YOUTUBEUNBLOCK -p udp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
iptables -t mangle -A POSTROUTING -j YOUTUBEUNBLOCK
iptables -I OUTPUT -m mark --mark 32768/32768 -j ACCEPT
```

### Iptables V.6 configuration if you needed
```text
ip6tables -t mangle -N YOUTUBEUNBLOCK
ip6tables -t mangle -A YOUTUBEUNBLOCK -p tcp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
ip6tables -t mangle -A YOUTUBEUNBLOCK -p udp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
ip6tables -t mangle -A POSTROUTING -j YOUTUBEUNBLOCK
ip6tables -I OUTPUT -m mark --mark 32768/32768 -j ACCEPT
```
### Download
```text
mkdir -p /tmp/dpi
cd /tmp/dpi
wget http://xerocop.ru/git/youtubeUnblock
chmod -R 777 /tmp/dpi
```


### Run youtubeUnblock
for Youtube only
```text
/tmp/dpi/youtubeUnblock &
```

for all sites
```text
/tmp/dpi/youtubeUnblock --sni-domains=all &
```

close telnet window

# LINKS
https://github.com/Waujito/youtubeUnblock