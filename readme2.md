1. chdir("/tmp")

2.
```
root@undistributed8:~# file /dev/tty
/dev/tty: character special (5/0)
root@undistributed8:~# file /dev/sda
/dev/sda: block special (8/0)
root@undistributed8:~# file /bin/bash
/bin/bash: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=2a9f157890930ced4c3ad0e74fc1b1b84aad71e6, for GNU/Linux 3.2.0, stripped
```
на основе man file можно сделать вывод что для магическая база данных находится в файлах 
```
The information identifying these files is read from /etc/magic and the compiled magic file
     /usr/share/misc/magic.mgc, or the files in the directory /usr/share/misc/magic if the compiled file does not
     exist.  In addition, if $HOME/.magic.mgc or $HOME/.magic exists, it will be used in preference to the system
     magic files.
```
Вывод strace это подтверждает.
```
stat("/root/.magic.mgc", 0x7ffc4a5c00a0) = -1 ENOENT (No such file or directory)
stat("/root/.magic", 0x7ffc4a5c00a0)    = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)
stat("/etc/magic", {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
read(3, "# Magic local data for file(1) c"..., 4096) = 111
read(3, "", 4096)                       = 0
close(3)                                = 0
openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3
```
3. 
4.
Процесс при завершении (как нормальном, так и в результате не обрабатываемого сигнала) освобождает все свои ресурсы и становится «зомби» — пустой записью в таблице процессов, хранящей статус завершения, предназначенный для чтения родительским процессом.

5.
6.
uname -a использует вызов uname()
```
uname({sysname="Linux", nodename="undistributed8", ...}) = 0
```
необходимо установить пакет manpages-dev, для просмотра мануалов по системным вызовам.
```
  Part of the utsname information is also accessible via /proc/sys/kernel/{ostype, hostname,  osrelease,  version, domainname}.
```

7.
```
; - последовательное выполнение команд(a;b;c;d)
&& - Операторы && являются управляющими операторами. Если в командной строке стоит command1 && command2, то command2 выполняется в том, и только в том случае, если статус выхода из команды command1 равен 0, что говорит об успешном ее завершении.
```
```
root@undistributed8:~# test -d /tmp/some_dir; echo Hi Hi
Hi Hi
root@undistributed8:~# test -d /tmp/some_dir && echo Hi Hi
root@undistributed8:~# mkdir /tmp/some_dir
root@undistributed8:~# test -d /tmp/some_dir && echo Hi Hi
Hi Hi
```
8.
9.
10.
11.

