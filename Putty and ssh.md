## Copy files with putty/pscp over ssh

```
# From windows, copy from a linux ssh connection
pscp -r username@serverip:/home/library/*.* ./
```

## OpenSSH change KEX
https://man.openbsd.org/ssh_config#Ciphers
<br>
https://man.openbsd.org/ssh_config#MACs
<br>
https://man.openbsd.org/ssh_config#KexAlgorithms
<br>
https://man.openbsd.org/ssh_config#PubkeyAcceptedKeyTypes
```
ssh -oKexAlgorithms=diffie-hellman-group1-sha1 username@192.168.1.2
```

