### INSTALL
```
[gandalf@mail-20040-rky ~]$ sudo dnf install postfix s-nail cyrus-sasl cyrus-sasl-plain -y
```

### UPDATE FILES
```
[root@mail-20040-rky ~]# vi /etc/postfix/sasl_passwd
[root@mail-20040-rky ~]# chmod 600 sasl_passwd 
[root@mail-20040-rky ~]# postmap sasl_passwd
[root@mail-20040-rky ~]# vi /etc/postfix/main.cf
```
### SEND MAILS
#### All in one line

`echo "Test Email TEXT" | mail -s "Send Email from Linux SUBJ" DESTEMAIL@gmail.com`

#### Type the body interactively
```
mail -s "Send Email from Linux" DESTEMAIL@gmail.com ENTER

huipizda
tratata
param pu pum
EOT
```
#### Attach a file
`echo "Test Email with attachment" | mail -s "Send Email from Linux with Attachment" -a message.txt DESTEMAIL@gmail.com`

#### Insert a timestamp into the SUBJECT
`DATE=$(date +%d-%b-%Y_at_%T) ; cat message.txt | mail -s "$DATE MAIL DELIVERY" DESTEMAIL@gmail.com`

