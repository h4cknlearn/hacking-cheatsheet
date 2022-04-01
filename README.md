# hacking-cheatsheet
📑 _A hacking cheat sheet to help you cover all the basic needs_

_ps: i'll be updating this cheat sheet every week_


## Simple file transfering using SFTP
```bash 
sftp user@remoteip
sftp > put file
```

that's all we need to transfer files from local machine to remote servers as easy as possible

## Extracting tar files
```bash
tar -xvf archive.tar
```
used to exctrat files commonly present in CTFs programs

## Verifying SHA256 checksum in linux
```bash
sha256sum <filename>
```

### Explaining /dev/null command in CTFs and privilege escalation techniques
```bash
<code here> 2>/dev/null
# /dev/null stands for null device on linux system, it operates just like a black hole, 
# throwing all outputs over there
```
`>` operator stands for redirection
`2` stands for error files

that's because all linux commands generates three main files associated with it

0 = standard input

1 = standard output

2 = standard error

So that's why 2>/dev/null is used to drop errors inside the Linux system's black hole.

## Simple kill process 
```bash
sudo kill <pid> 
```

## Using a simple SOCKS Proxy
```bash
ssh <remoteip> -l <username> -D 127.0.0.1:1080
# -D enables socks proxy binding our machine's traffic with the remote one
```
We can use it along Burp Suite to forward all the VPS's traffic through our local machine
using the burp's proxy on the local browser at the same time

`ps: here you will need to configure burp as well`

## Anonymous login
```bash
ftp <target ip address>
username: anonymous
password: [enter key]
```

## smbclient
```bash
# connects to the target listing all the shared documents
smbclient -N -L \\\\target ip\\ # -N supress the password prompt
smbclient -N \\\\target ip\\openshares

get <file> # downloads the file
more <file> # outputs the content file without the needing to download 
# in our local machine
```

## User enum and permissions
```bash
sudo -l # checks which commands we can execute on the system
id # checks users permissions

find / -group <groupname> 2>/dev//null # to find a specific group name
```

## Upgrading our shell
```bash 
python -c 'import pty; pty.spawn("/bin/bash")'
# here pty module let's us spawn a pseudo terminal
```
