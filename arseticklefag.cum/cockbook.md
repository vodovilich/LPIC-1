### Install bind
`gandalf@dns-20053-ubnt:~$ sudo apt install bind9 -y`

### Forward zone
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo vi arseticklefag.cum.forward
;ORIGIN if not specified - taken from named.conf file
$ORIGIN arseticklefag.cum.

$TTL    86400
@       IN      SOA     dns-20053-ubnt.arseticklefag.cum. huiadmin.arseticklefag.cum. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         86400 )        ; Negative Cache TTL
;
@               IN      NS      dns-20053-ubnt.arseticklefag.cum.

@               IN      A       192.168.200.53
dns-20053-ubnt  IN      A       192.168.200.53
```

### Reverse zone
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo vi arseticklefag.cum.200.reverse
$ORIGIN 200.168.192.in-addr.arpa.
$TTL    86400

@       IN      SOA     dns-20053-ubnt.arseticklefag.cum. huiadmin.arseticklefag.cum. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                          86400 )       ; Negative Cache TTL
;
@       IN      NS      dns-20053-ubnt.arseticklefag.cum.

53      IN      PTR     dns-20053-ubnt.arseticklefag.cum.

```

### named.conf.local
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo vi named.conf.local
zone "arseticklefag.cum" {
        type master;
        file "/etc/bind/arseticklefag.cum.forward";
};

zone "200.168.192.in-addr.arpa" {
        type master;
        file "/etc/bind/arseticklefag.cum.200.reverse";

};
```

### named.conf.options

```
gandalf@dns-20053-ubnt:/etc/bind$ sudo vi named.conf.options
options {
        directory "/var/cache/bind";

        forwarders {
                8.8.8.8;
                1.1.1.1;
        };

        listen-on { any; };
        allow-query { any; };
        allow-recursion { any; };
        dnssec-validation auto;

        listen-on-v6 { any; };
};
```

### Verify 
- **named-checkconf** - named configuration file syntax checking tool
  - named-checkconf  checks the syntax, but not the semantics, of a named configuration file.
    - The file, along with all files  included by it, is parsed and checked for syntax errors.
  - If no file is specified, /etc/bind/named.conf is  read  by  default.
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo named-checkconf
gandalf@dns-20053-ubnt:/etc/bind$ echo $?
0
```
- **named-checkzone** - zone file validity checking or converting tool
  - Checks the syntax and integrity of a zone file.
    - Performs the same checks as named does when loading a zone.
  - Useful for checking zone files before configuring them into a name server.
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo named-checkzone 200.168.192.in-addr.arpa /etc/bind/arseticklefag.cum.200.reverse
zone 200.168.192.in-addr.arpa/IN: loaded serial 1
OK
```
### RNDC
- rndc included into bind-utils package
```
gandalf@dns-20053-ubnt:/etc/bind$ which rndc
/usr/sbin/rndc
gandalf@dns-20053-ubnt:/etc/bind$ sudo apt install apt-file -y
gandalf@dns-20053-ubnt:/etc/bind$ sudo apt-file update
gandalf@dns-20053-ubnt:/etc/bind$ sudo apt-file search /usr/sbin/rndc
bind9-utils: /usr/sbin/rndc
bind9-utils: /usr/sbin/rndc-confgen
```
- Updates a zone without restarting the named service
```
$ sudo rndc reconfig
$ sudo rndc reload atffc.hui
$ sudo rndc reload
```
