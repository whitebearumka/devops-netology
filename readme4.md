
1.
2.
3.Все получилось успешно

![Settings Window](https://github.com/whitebearumka/devops-netology/blob/main/Screenshot_11.png)

4.
```
root@vagrant:~# dmesg | grep virt
[    0.007726] CPU MTRRs all blank - virtualized system.
[    0.059869] Booting paravirtualized kernel on KVM
[    0.671609] Performance Events: PMU not available due to virtualization, using software events only.
[   13.261629] systemd[1]: Detected virtualization oracle.
```
dmesg показывает что система запускается в виртуальной среде KVM от oracle.
В отличии от другой системы которая работает в WSL2
```
root@undistributed8:~# dmesg | grep virt
[    0.045678] Booting paravirtualized kernel on Hyper-V
[    0.147874] Performance Events: PMU not available due to virtualization, using software events only.
```
Где показывается что система запускается в паравиртуализации от Hyper-V.

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
Если попробовать разложить эту строку ``:(){ :|:& };:``
```
:() \\определение функции :
{\\начало функции :
:|:& \\функция : вызывает саму себя и передает управление самой себе при этом работая в фоновом процессе 
};\\конец функции :
:
```
защита системы сработала 
```
root@vagrant:~# dmesg|grep  fork
[ 1412.239602] cgroup: fork rejected by pids controller in /user.slice/user-1000.slice/session-3.scope
```
cgroups (англ. control group) — механизм ядра Linux, который ограничивает и изолирует вычислительные ресурсы (процессорные, сетевые, ресурсы памяти, ресурсы ввода-вывода) для групп процессов. Механизм позволяет образовывать иерархические группы процессов с заданными ресурсными свойствами и обеспечивает программное управление ими.

7.

