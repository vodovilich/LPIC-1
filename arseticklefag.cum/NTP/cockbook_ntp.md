### Install chrony:
`gandalf@ntp-20020-ubnt:~$ sudo apt install chrony -y`

### mask systemd-timesyncd on Ubuntu:
`gandalf@ntp-20020-ubnt:~$ sudo systemctl stop systemd-timesyncd`  
`gandalf@ntp-20020-ubnt:~$ sudo systemctl mask systemd-timesyncd`

- If needed - fix the failed masked sysd-unit status:
`gandalf@ntp-20020-ubnt:~$ sudo systemctl reset-failed systemd-timesyncd`
  
### Setup a key:
```
gandalf@ntp-20020-ubnt:~$ base64 <<< arseticklefagg
YXJzZXRpY2tsZWZhZ2cK
gandalf@ntp-20020-ubnt:~$ sudo vi /etc/chrony/chrony.keys
101 MD5 YXJzZXRpY2tsZWZhZ2cK
```

### Update Server config:
`gandalf@ntp-20020-ubnt:~$ echo 'allow 192.168.0.0/16' | sudo tee -a /etc/chrony/chrony.conf`

### Update Client config:
```
[gandalf@mail-20040-rky ~]$ sudo vi /etc/chrony.conf
#pool 2.rocky.pool.ntp.org iburst
server ntp-20020-ubnt.arseticklefag.cum iburst key 101
```

### Configure Cisco:
```
sw-left-20050(config)#ntp authentication-key 101 md5 YXJzZXRpY2tsZWZhZ2cK
sw-left-20050(config)#ntp authenticate
sw-left-20050(config)#ntp trusted-key 101
sw-left-20050(config)#ntp source Vlan100
sw-left-20050(config)#ntp server 192.168.200.20 key 101
```


### Configure Juniper:
```
root@sw-right-20060> set date 202601032109.30
root@sw-right-20060# set system time-zone UTC

root@sw-right-20060# set system ntp authentication-key 101 type md5 value YXJzZXRpY2tsZWZhZ2cK
root@sw-right-20060# set system ntp server 192.168.200.20
root@sw-right-20060# set system ntp source-address 192.168.200.60

root@sw-right-20060> set date ntp
root@sw-right-20060> set date ntp force
```

