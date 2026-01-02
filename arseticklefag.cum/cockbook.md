# Install bind

#Forward zone

#Reverse zone

#named.conf.local

#named.conf.options

#Verify 
- named-checkconf - named configuration file syntax checking tool
  - named-checkconf  checks the syntax, but not the semantics, of a named configuration file.
    - The file, along with all files  included by it, is parsed and checked for syntax errors.
  - If no file is specified, /etc/bind/named.conf is  read  by  default.
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo named-checkconf
gandalf@dns-20053-ubnt:/etc/bind$ echo $?
0
```
- named-checkzone - zone file validity checking or converting tool
  - Checks the syntax and integrity of a zone file.
    - Performs the same checks as named does when loading a zone.
  - Useful for checking zone files before configuring them into a name server.
```
gandalf@dns-20053-ubnt:/etc/bind$ sudo named-checkzone 200.168.192.in-addr.arpa /etc/bind/arseticklefag.cum.200.reverse
zone 200.168.192.in-addr.arpa/IN: loaded serial 1
OK
```
#RNDC
```
$ sudo rndc reconfig
$ sudo rndc reload atffc.hui
```
