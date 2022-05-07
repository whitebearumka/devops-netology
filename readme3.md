1.
```
root@undistributed8:~# telnet stackoverflow.com 80
Trying 151.101.129.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 71e5455f-f540-446b-b62b-851e0d745288
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Sat, 07 May 2022 10:39:31 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-hel1410030-HEL
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1651919972.726583,VS0,VE110
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=8507b53a-9d99-6d19-976d-304af57ac320; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
2.
3.
```
136.169.173.181
```
4.
```
% Information related to '136.169.173.0/24AS24955'

route:          136.169.173.0/24
descr:          JSC "Ufanet", Ufa, Russia
origin:         AS24955
mnt-by:         UBN-MNT
created:        2013-07-08T12:18:31Z
last-modified:  2013-07-08T12:18:31Z
source:         RIPE

```
5.
6.
```
                                                   My traceroute  [v0.93]
undistributed8 (172.23.88.111)                                                                     2022-05-07T16:49:57+0500
Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                                                   Packets               Pings
 Host                                                                            Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. AS???    undistributed8.mshome.net                                            0.0%     5    0.3   0.5   0.3   0.8   0.2
 2. AS???    192.168.0.1                                                          0.0%     5    2.3   2.8   2.3   3.8   0.7
 3. AS???    100.94.128.1                                                         0.0%     5    3.1   9.8   3.1  17.1   6.8
 4. AS???    10.1.230.99                                                          0.0%     5    2.6   2.8   2.6   3.0   0.2
 5. AS???    10.1.230.113                                                         0.0%     5    3.2   6.4   3.2  15.4   5.1
 6. AS???    10.0.22.81                                                           0.0%     5    4.2  14.8   4.2  29.5  11.9
 7. AS???    10.0.22.10                                                           0.0%     5    5.1   9.6   4.9  23.8   8.0
 8. AS???    10.0.20.25                                                           0.0%     5    7.0   7.5   5.9   9.9   1.5
 9. AS???    10.0.20.21                                                           0.0%     5    9.6  10.1   6.7  18.3   4.7
10. AS???    10.2.3.17                                                            0.0%     5    4.7   5.9   4.3   8.8   2.0
11. AS???    10.1.84.33                                                           0.0%     5    7.3   9.3   5.1  22.0   7.2
12. AS???    10.1.65.22                                                           0.0%     5    5.5   6.7   4.4  14.5   4.4
13. AS???    10.1.65.65                                                           0.0%     5    9.6   7.7   5.2   9.6   1.9
14. AS???    10.3.2.3                                                             0.0%     5   23.9  28.2  23.9  32.6   3.2
15. AS15169  72.14.220.188                                                        0.0%     5   30.4  28.0  26.9  30.4   1.4
16. AS15169  142.251.68.223                                                       0.0%     5   33.4  31.6  26.3  34.0   3.2
17. AS15169  108.170.250.99                                                       0.0%     5   31.0  30.4  27.1  33.0   2.4
18. AS15169  142.251.238.82                                                       0.0%     4   51.4  52.2  44.8  67.1  10.4
19. AS15169  142.251.238.68                                                       0.0%     4   62.5  51.0  42.6  62.5   9.0
20. AS15169  172.253.51.187                                                       0.0%     4   42.1  47.1  42.0  60.4   8.9
21. (waiting for reply)
22. (waiting for reply)
23. (waiting for reply)
24. (waiting for reply)
25. (waiting for reply)
26. (waiting for reply)
27. (waiting for reply)
28. (waiting for reply)
29. (waiting for reply)
30. AS15169  dns.google                                                           0.0%     4   42.5  49.0  42.5  63.5   9.8
```
Если орентироватся на максимальное среднее время задержки то это 18 хоп (Максимальное среднее время задержки 52 мс)
```
18. AS15169  142.251.238.82                                                       0.0%     4   51.4  52.2  44.8  67.1  10.4
```
7.
NS-записи
```
root@undistributed8:~# dig dns.google NS

; <<>> DiG 9.16.1-Ubuntu <<>> dns.google NS
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44937
;; flags: qr rd ad; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;dns.google.                    IN      NS

;; ANSWER SECTION:
dns.google.             0       IN      NS      ns1.zdns.google.
dns.google.             0       IN      NS      ns4.zdns.google.
dns.google.             0       IN      NS      ns3.zdns.google.
dns.google.             0       IN      NS      ns2.zdns.google.

;; Query time: 180 msec
;; SERVER: 172.23.80.1#53(172.23.80.1)
;; WHEN: Sat May 07 17:05:09 +05 2022
;; MSG SIZE  rcvd: 154
```
A-записи
```
root@undistributed8:~# dig dns.google A

; <<>> DiG 9.16.1-Ubuntu <<>> dns.google A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47127
;; flags: qr rd ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;dns.google.                    IN      A

;; ANSWER SECTION:
dns.google.             0       IN      A       8.8.8.8
dns.google.             0       IN      A       8.8.4.4

;; Query time: 0 msec
;; SERVER: 172.23.80.1#53(172.23.80.1)
;; WHEN: Sat May 07 17:06:05 +05 2022
;; MSG SIZE  rcvd: 70
```
8.
Запрос PTR-записи для 8.8.8.8
```
root@undistributed8:~# dig -x 8.8.8.8

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22905
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 0 msec
;; SERVER: 172.23.80.1#53(172.23.80.1)
;; WHEN: Sat May 07 17:08:04 +05 2022
;; MSG SIZE  rcvd: 82
```
Запрос PTR-записи для 8.8.4.4
```
root@undistributed8:~# dig -x 8.8.4.4

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 3078
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 190 msec
;; SERVER: 172.23.80.1#53(172.23.80.1)
;; WHEN: Sat May 07 17:09:42 +05 2022
;; MSG SIZE  rcvd: 82
```
Привязано доменное имя dns.google.
