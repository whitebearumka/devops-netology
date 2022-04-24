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
```
ls % 2>/dev/tty2
```
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
```
root@undistributed8://root/3/1# bash 5>&1
root@undistributed8://root/3/1#
```
Мы временно переназначили файловый дискриптор 5 на вывод STDOUT(1). Поэтому при выполнении
```
echo netology > /proc/$$/fd/5
```
сообщение netology попадет в STDOUT(1).
8.

9. Выведет все текущие пременные окружения, аналог команды "env"
10.

11.
```
cat /proc/cpuinfo|grep -io ' sse[0-9]'|sort -r|uniq|sed '1!d'
```
Команда анализирует наличие инструкций SSE и выводит самую старшую (sort -r) и только одну (sed '1!d') версию набора инструкций SSE. 
12. Никаких ошибок как в задании.

13. Все получилось. Желательно делать из права root и по умолчанию перетаскивает 1 процесс. Как вариант можно использовать ключ -T для переноса всей терминальной сессии.

14.
