1. cd-команда оболочки shell по факту выполняющая функцию chdir(). узнать об этом возможно при помощи type
```
root@undistributed8://root/3/1# type cd
cd is a shell builtin
```
2. Команда "grep <some_string> <some_file> | wc -l" выводит количество строк в которых есть значение <some_string> в файле <some_file>. Аналогом этого может выступать команда grep c ключом -с.
```
root@undistributed8://root/3/1# grep 8 111 | wc -l
6
root@undistributed8://root/3/1# grep -c  8 111
6
```
3. 
```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0    900   528 ?        Sl   Apr22   0:00 /init
```
4.
5.
```
root@undistributed8://root/3/1# cat 123
7
3
2
6
1
root@undistributed8://root/3/1# sort < 123 > 1234
root@undistributed8://root/3/1# cat 1234
1
2
3
6
7
```
6.
7.
8.
9. Выведет все текущие пременные окружения, аналог команды "env"
10.
11.
12.
13.
14.
