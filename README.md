# hacking-cheatsheet
A hacking cheat sheet to help you cover all the basic needs


## Simple file transfering using SFTP
```bash 
sftp user@remoteip
sftp > put file
```

that's all we need to transfer files from local machine to remote servers

## Extracting tar files
```bash
tar -xvf archive.tar
```
used to exctrat files commonly present in CTFs programs

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



