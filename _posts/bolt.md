![image](https://user-images.githubusercontent.com/63084488/135747679-05e70a7c-329d-41f3-85f6-2775430a3e02.png)

```bash
# Nmap 7.91 scan initiated Sun Oct  3 12:57:43 2021 as: nmap -vvv -p 22,80,443 -A -sV -sC -oN nmaprust.txt 10.10.11.114
Nmap scan report for 10.10.11.114
Host is up, received echo-reply ttl 63 (0.33s latency).
Scanned at 2021-10-03 12:57:44 +04 for 42s

PORT    STATE SERVICE  REASON         VERSION
22/tcp  open  ssh      syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 4d:20:8a:b2:c2:8c:f5:3e:be:d2:e8:18:16:28:6e:8e (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDkj3wwSWqzkYHp9SbRMcsp8vHlgm5tTmUs0fgeuMCowimWCqCWdN358ha6zCdtC6kHBD9JjW+3puk65zr2xpd/Iq2w+UZzwVR070b3eMYn78xq+Xn6ZrJg25e5vH8+N23olPkHicT6tmYxPFp+pGo/FDZTsRkdkDWn4T2xzWLjdq4Ylq+RlXmQCmEsDtWvNSp3PG7JJaY5Nc+gFAd67OgkH5TVKyUWu2FYrBc4KEWvt7Bs52UftoUTjodRYbOevX+WlieLHXk86OR9WjlPk8z40qs1MckPJi926adEHjlvxdtq72nY25BhxAjmLIjck5nTNX+11a9i8KSNQ23Fjs4LiEOtlOozCFYy47+2NJzFi1iGj8J72r4EsEY+UMTLN9GW29Oz+10nLU1M+G6DQDKxoc1phz/D0GShJeQw8JhO0L+mI6AQKbn0pIo3r9/hLmZQkdXruJUn7U/7q7BDEjajVK3gPaskU/vPJRj3to8g+w+aX6IVSuVsJ6ya9x6XexE=
|   256 7b:0e:c7:5f:5a:4c:7a:11:7f:dd:58:5a:17:2f:cd:ea (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBF5my/tCLImcznAL+8z7XV5zgW5TMMIyf0ASrvxJ1mnfUYRSOGPKhT8vfnpuqAxdc5WjXQjehfiRGV6qUjoJ3I4=
|   256 a7:22:4e:45:19:8e:7d:3c:bc:df:6e:1d:6c:4f:41:56 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGxr2nNJEycZEgdIxL1zHLHfh+IBORxIXLX1ciHymxLO
80/tcp  open  http     syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 76362BB7970721417C5F484705E5045D
| http-methods: 
|_  Supported Methods: HEAD GET OPTIONS
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title:     Starter Website -  About 
443/tcp open  ssl/http syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 82C6406C68D91356C9A729ED456EECF4
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-title: Passbolt | Open source password manager for teams
|_Requested resource was /auth/login?redirect=%2F
| ssl-cert: Subject: commonName=passbolt.bolt.htb/organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=AU
| Issuer: commonName=passbolt.bolt.htb/organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=AU
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-02-24T19:11:23
| Not valid after:  2022-02-24T19:11:23
| MD5:   3ac3 4f7c ee22 88de 7967 fe85 8c42 afc6
| SHA-1: c606 ca92 404f 2f04 6231 68be c4c4 644f e9ed f132
| -----BEGIN CERTIFICATE-----
| MIIDozCCAougAwIBAgIUWYR6DcMDhx5i4CpQ5qkkspuUULAwDQYJKoZIhvcNAQEL
| BQAwYTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUxITAfBgNVBAoM
| GEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDEaMBgGA1UEAwwRcGFzc2JvbHQuYm9s
| dC5odGIwHhcNMjEwMjI0MTkxMTIzWhcNMjIwMjI0MTkxMTIzWjBhMQswCQYDVQQG
| EwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UECgwYSW50ZXJuZXQgV2lk
| Z2l0cyBQdHkgTHRkMRowGAYDVQQDDBFwYXNzYm9sdC5ib2x0Lmh0YjCCASIwDQYJ
| KoZIhvcNAQEBBQADggEPADCCAQoCggEBALPBsFKzUPba5tHWW85u/Do3CkSsUgWN
| Wp5ZShD3T3hRX+vxFjv0zVZaccLhY8gsoTaklvFZVrguU6rIKHCFpRt7JLSPCmx3
| /Dy8id1Fm3VgRStVcMdXFnWne3lZaw9cSqdAxzb6ZcERAZRlIOPj29zO5UIwvwTW
| FJwybndHlxZ9Y8TUT7O1z5FFNKMl/QP6DBdkDDTc+OQ9ObyYHd6zBdwfuJykX8Md
| 3ejO1n38j8zXhzB/DEwKVKqFqvm7K28OBOouOaHnqM5vO5OVEVNyeZhaOtX1UrOm
| c+B8RSHDU7Y7/6sbNxJGuwpJZtovUa+2HybDRJl92vnNeouddrdFZc0CAwEAAaNT
| MFEwHQYDVR0OBBYEFCjzBazWUuLcpQnqbcDsisjmzvYzMB8GA1UdIwQYMBaAFCjz
| BazWUuLcpQnqbcDsisjmzvYzMA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQEL
| BQADggEBAA2qDGXEgqNsf4XqYqK+TLg+pRJ/rrdAFtxNwn8MYQv4ZlyouQsN2zPm
| t/dXls0iba1KvgYrt5QGWGODI8IkaujEDC452ktOmmi9+EnpK9DjKoKfCTL4N/ta
| xDZxR4qHrk35QVYB8jYVP8S98gu5crTkAo9TGiHoEKPvinx+pA9IHtynqh9pBbuV
| /micD+zMBVlZ50MILbcXqsBHRxHN4pmbcfc4yEOanNVJD3hmGchcyAFx2RLPsl36
| +QrGlwqpP7Bn7wzVCuxzQUWlA9VwVZKHYVVvCekvVP9DKL6FfI5avLgJJujQTqKw
| +uYRUUWj+CdI1oxxYt0SdimXHr81SgE=
|_-----END CERTIFICATE-----
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 4.15 - 5.6 (95%), Linux 5.3 - 5.4 (95%), Linux 2.6.32 (95%), Linux 5.0 - 5.3 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 5.0 - 5.4 (93%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.91%E=4%D=10/3%OT=22%CT=%CU=43223%PV=Y%DS=2%DC=T%G=N%TM=615970B2%P=x86_64-pc-linux-gnu)
SEQ(SP=102%GCD=1%ISR=10C%TI=Z%CI=Z%II=I%TS=A)
OPS(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST11NW7%O6=M54DST11)
WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)
ECN(R=Y%DF=Y%T=40%W=FAF0%O=M54DNNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 41.056 days (since Mon Aug 23 11:37:36 2021)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=258 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   183.77 ms 10.10.14.1
2   585.65 ms 10.10.11.114

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Oct  3 12:58:27 2021 -- 1 IP address (1 host up) scanned in 44.29 seconds
```
Nmap reveals three open ports, virtual host name from SSL certificate. Let’s add it to your hosts 
file and visit the webpage.



![image](https://user-images.githubusercontent.com/63084488/135747929-10b0e398-15b1-4279-8235-18b22a0ff701.png)

lloged in as admin with password
![image](https://user-images.githubusercontent.com/63084488/135748441-fb3fb93f-6c34-42a8-b036-489ee210e15a.png)

chat 
![image](https://user-images.githubusercontent.com/63084488/135748519-9d6e2015-5e29-47c4-a208-71016173e819.png)

```
gobuster vhost -u http://bolt.htb -t 30 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:          http://bolt.htb
[+] Method:       GET
[+] Threads:      30
[+] Wordlist:     /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
[+] User Agent:   gobuster/3.1.0
[+] Timeout:      10s
===============================================================
2021/10/03 14:03:37 Starting gobuster in VHOST enumeration mode
===============================================================
Found: mail.bolt.htb (Status: 200) [Size: 4943]
Found: demo.bolt.htb (Status: 302) [Size: 219] 
                                               
===============================================================
2021/10/03 14:04:53 Finished
===============================================================
```
![image](https://user-images.githubusercontent.com/63084488/135749090-50bb0b6c-014b-45db-8a25-5b52761e1e72.png)


