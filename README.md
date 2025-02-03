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
iptables -t mangle -A YOUTUBEUNBLOCK -p udp -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:8 -j NFQUEUE --queue-num 537 --queue-bypass
iptables -t mangle -A POSTROUTING -j YOUTUBEUNBLOCK
iptables -I OUTPUT -m mark --mark 32768/32768 -j ACCEPT
```

### Iptables V.6 configuration if you needed
```text
ip6tables -t mangle -N YOUTUBEUNBLOCK
ip6tables -t mangle -A YOUTUBEUNBLOCK -p tcp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
ip6tables -t mangle -A YOUTUBEUNBLOCK -p udp -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:8 -j NFQUEUE --queue-num 537 --queue-bypass
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
/tmp/dpi/youtubeUnblock --fake-sni-type=custom --fake-custom-payload=00 --fake-sni-seq-len=10 --frag-sni-faked=1 --frag-sni-reverse=0 --frag-sni-pos=1 --frag-middle-sni=0 --seg2delay=100 &
```

for all sites
```text
/tmp/dpi/youtubeUnblock --fake-sni-type=custom --fake-custom-payload=00 --fake-sni-seq-len=10 --frag-sni-faked=1 --frag-sni-reverse=0 --frag-sni-pos=1 --frag-middle-sni=0 --seg2delay=100 --sni-domains=all &
```

close telnet window

# LINKS
https://github.com/Waujito/youtubeUnblock