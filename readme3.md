1.
```
root@undistributed8:~# telnet stackoverflow.com 80
Trying 151.101.129.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently //HTTP времено перемещен
cache-control: no-cache, no-store, must-revalidate //Нужно ли кешировать(В кеше не должно сохраняться ничего — ни по запросам клиента, ни по ответам сервера. Запрос всегда отправляется на сервер, ответ всегда загружается полностью.)
location: https://stackoverflow.com/questions //Просим браузер загрузить страницу HTTPS https://stackoverflow.com/questions
x-request-guid: 71e5455f-f540-446b-b62b-851e0d745288 //Идентификатор запроса на сервере.
feature-policy: microphone 'none'; speaker 'none'// Требуется ли включить микрофон(НЕТ),Нужно ли включить динамик(НЕТ).
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com //Включена политика защиты контента(upgrade-insecure-requests который обяжет браузеры, которые поддерживают спецификацию Upgrade-Insecure-Requests, отправлять запросы на сайт в защищенном режиме. Фреймы разрешены только с https://stackexchange.com)
Accept-Ranges: bytes//В Accept-Ranges HTTP заголовок ответа является маркером , используемым сервером , чтобы рекламировать свою поддержку частичных запросов от клиента для загрузки файлов. Значение этого поля указывает единицу измерения, которую можно использовать для определения диапазона.
Date: Sat, 07 May 2022 10:39:31 GMT//Дата и время
Via: 1.1 varnish//Сервер использует Varnish HTTP Cache.
Connection: close//Соединение закрыто
X-Served-By: cache-hel1410030-HEL //Этот заголовок предоставляет идентификаторы сервера защиты и узла локального кэша, где запрос ищет данные.
X-Cache: MISS//Обычно имеет два значения (например, «X-Cache: MISS, MISS»). Первое значение указывает, доступен ли кэш на защищенном сервере, а второе указывает, доступен ли он на локальном сервере кэша.
X-Cache-Hits: 0//Этот заголовок, как и заголовок «X-Cache», помогает определить, был ли запрос обслужен из локального центра обработки данных CDN или исходного сервера
X-Timer: S1651919972.726583,VS0,VE110 //Время от Varnish HTTP Cache (	Sat May 07 2022 10:39:32 GMT+0000)
Vary: Fastly-SSL//Заголовок ответа Vary сообщает кэшам, что определенный заголовок (или заголовки) из запроса следует использовать, чтобы сделать ключ кэша для объекта более конкретным. В данном случае что используется TLS от облачной компании Fastly.
X-DNS-Prefetch-Control: off//Не указывать сервера для нахождения контента. запросы будут идти через DNS.
Set-Cookie: prov=8507b53a-9d99-6d19-976d-304af57ac320; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly//Отправить куки на агент со сроком до 1 января 2055года.

Connection closed by foreign host.
```
2.
Первый ответ сервера 
```
Status Code: 307 Internal Redirect
```
Полный ответ HTTP сервера
```
HTTP/1.1 307 Internal Redirect
Location: https://stackoverflow.com/
Cross-Origin-Resource-Policy: Cross-Origin
Non-Authoritative-Reason: HSTS
```
Самый долгий запрос 4.03 секунды
```
Request URL: https://stats.g.doubleclick.net/j/collect?t=dc&aip=1&_r=3&v=1&_v=j96&tid=UA-108242619-1&cid=1081787660.1651930870&jid=1314158479&gjid=821821134&_gid=30943335.1651930870&_u=SCCACEAAFAAAAC~&z=1112844665
Referrer Policy: strict-origin-when-cross-origin
```

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
```
root@undistributed8:~# traceroute -IAn 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  172.23.80.1 [*]  3.823 ms  1.680 ms  1.670 ms
 2  192.168.31.1 [*]  6.601 ms  6.601 ms  6.600 ms
 3  100.103.0.1 [*]  6.923 ms  6.921 ms  5.858 ms
 4  10.2.3.17 [*]  5.842 ms  5.841 ms  5.725 ms
 5  10.1.84.65 [*]  11.353 ms  11.332 ms *
 6  * 10.1.67.135 [*]  8.578 ms  8.550 ms
 7  10.1.67.193 [*]  10.000 ms  3.373 ms  3.356 ms
 8  10.1.190.62 [*]  3.354 ms  3.352 ms  3.352 ms
 9  10.3.1.13 [*]  34.738 ms  34.736 ms  34.734 ms
10  72.14.220.188 [AS15169]  34.733 ms  34.733 ms  34.732 ms
11  108.170.250.33 [AS15169]  34.730 ms  32.397 ms  32.384 ms
12  108.170.250.34 [AS15169]  25.342 ms  25.341 ms  63.962 ms
13  142.251.238.82 [AS15169]  64.026 ms  64.024 ms  64.023 ms
14  142.251.238.72 [AS15169]  63.946 ms  63.945 ms  63.944 ms
15  172.253.79.237 [AS15169]  63.943 ms  63.942 ms  63.940 ms
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  8.8.8.8 [AS15169]  47.388 ms  49.068 ms  49.067 ms
```

6.
```
                                                 My traceroute  [v0.93]
undistributed8 (172.23.82.181)                                                                 2022-05-10T23:09:54+0500
Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                                               Packets               Pings
 Host                                                                        Loss%   Snt   Last   Avg  Best  Wrst StDev
 1. AS???    172.23.80.1                                                      0.0%   144    0.3   0.4   0.2   1.1   0.1
 2. AS???    192.168.31.1                                                     0.0%   144    1.4   5.4   1.1  99.9  12.4
 3. AS???    100.103.0.1                                                      0.0%   144    1.8   6.8   1.5  93.0  11.5
 4. AS???    10.2.3.17                                                        0.0%   144    2.0   5.7   1.7  52.5   7.0
 5. AS???    10.1.84.65                                                      22.4%   144    2.6   7.2   2.1  97.0  12.7
 6. AS???    10.1.67.135                                                     18.1%   144    1.8   8.5   1.6  97.9  15.2
 7. AS???    10.1.67.193                                                      0.0%   144    2.3   6.5   1.7  57.6   8.8
 8. AS???    10.1.190.62                                                      0.7%   144    2.8   6.2   1.8  80.0   8.5
 9. AS???    10.3.1.13                                                        0.0%   144   32.7  37.4  28.7 173.7  19.6
10. AS15169  72.14.220.188                                                    1.4%   144   29.6  35.4  29.1 134.2  14.7
11. AS15169  108.170.250.33                                                   1.4%   144   34.0  35.9  30.0 153.1  14.8
12. AS15169  108.170.250.34                                                   1.4%   144   28.1  31.4  24.5 126.3  15.4
13. AS15169  142.251.238.82                                                   0.0%   144   58.4  54.0  47.3 170.6  12.8
14. AS15169  142.251.238.72                                                   1.4%   144   50.6  54.1  47.2 173.7  14.7
15. AS15169  172.253.79.237                                                   0.7%   144   46.4  51.0  46.0 133.5  10.9
16. (waiting for reply)
17. (waiting for reply)
18. (waiting for reply)
19. (waiting for reply)
20. (waiting for reply)
21. (waiting for reply)
22. (waiting for reply)
23. (waiting for reply)
24. (waiting for reply)
25. AS15169  8.8.8.8                                                          0.7%   143   51.7  52.3  46.3 184.9  17.5
```
Если орентироватся на максимальное среднее время задержки то это 14 хоп (Максимальное среднее время задержки 54.1 мс)
```
14. AS15169  142.251.238.72                                                   1.4%   144   50.6  54.1  47.2 173.7  14.7
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
