### NETPLAN STATIC IP
```
sudo vi /etc/netplan/10-static.yaml
network:
    ethernets:
        ens3:
          addresses:
            - 192.168.200.53/24
          routes:
            - to: default
              via: 192.168.200.1
          dhcp4: false
    version: 2
```

### NM STATIC IP
```
sudo nmcli con edit ens3
>print ipv4
>set ipv4.method manual
>set ipv4.addresses 192.168.200.40/24
>set ipv4.gateway 192.168.200.1
>set ipv4.dns 8.8.8.8
>print ipv4
>quit

sudo nmcli con down ens3
sudo nmcli con up ens3
```

### DNS
```
sudo vi /etc/resolv.conf
nameserver 8.8.8.8
search arseticklefag.cum

sudo hostnamectl set-hostname dns-20053-ubnt
```

### APT
- Comment out the cdrom line  
`sudo vi /etc/apt/sources.list`

### NTP
```
sudo timedatectl set-timezone list-timezones | grep -i utc
sudo timedatectl set-timezone UTC
```
