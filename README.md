# youtubeUnblock on TP-Link Archer AX1500

## Get telnet root

https://github.com/gmaxus/TP-Link-Archer-AX1500-telnet-root

### Telnet to router
```text
telnet 192.168.0.1
```

### Download
```text
mkdir -p /tmp/dpi/var/lock
cd /tmp/dpi
wget http://thisismypage.ru/gitz/youtubeUnblock_0.3.2-model_brcm_bcm490x-1_model_brcm_bcm490x.ipk
```

### Install
```text
opkg install youtubeUnblock_0.3.2-model_brcm_bcm490x-1_model_brcm_bcm490x.ipk -o /tmp/dpi --force-depends --nodeps
```

### Iptables configuration
```text
iptanles -t mangle -A FORWARD -p tcp --dport 443 -m connbytes --connbytes-dir original --connbytes-mode packets --connbytes 0:19 -j NFQUEUE --queue-num 537 --queue-bypass
iptanles -I OUTPUT -m mark 32768/32768 -j ACCEPT
```

### Run youtubeUnblock
For Youtube only.
```text
/tmp/dpi/youtubeUnblock
```

For all sites.
```text
/tmp/dpi/youtubeUnblock --sni-domains=all
```

# LINKS
https://github.com/Waujito/youtubeUnblock