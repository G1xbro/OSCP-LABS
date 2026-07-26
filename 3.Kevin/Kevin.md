# Kevin Lab
## Reconnaissance
### All port scanning
### TCP
- `nmap -p- -T4 -sS --min-rate 1000 -oN Results_tcp.txt 192.168.102.45`
```text
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
```text
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
```
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
## Exploitation
### Web
We got in using default username and password = **'admin'**