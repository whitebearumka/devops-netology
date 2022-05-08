
1.
2.
3.
4.
5.
```
root@undistributed8:~# /sbin/sysctl -n fs.nr_open
1048576
```
данный параметр ядра овечает за лимит количество открытых дескрипторов на пользователя. nr_open - жесткий лимит на открытые дескрипторы. 
Для ограничения есть еще понятие "мягкий лимит" (ulimit -Sn) в отличии от "жесткого лимита"(ulimit -Hn).
```
root@vagrant:~# ulimit -n
1024
root@vagrant:~# ulimit -Sn
1024
root@vagrant:~# ulimit -Hn
1048576
root@vagrant:~# ulimit -n 1048577
-bash: ulimit: open files: cannot modify limit: Operation not permitted
```
Увеличить лимит больше чем fs.nr_open нельзя.
6.
7.
