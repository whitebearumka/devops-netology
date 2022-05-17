1. ## Узнайте о sparse (разряженных) файлах.
Разрежённый файл (англ. sparse file) — файл, в котором последовательности нулевых байтов заменены на информацию об этих последовательностях.
Преимущества:
экономия дискового пространства. Использование разрежённых файлов считается одним из способов сжатия данных на уровне файловой системы;
отсутствие временных затрат на запись нулевых байт;
увеличение срока службы запоминающих устройств.
Недостатки:
накладные расходы на работу со списком дыр;
фрагментация файла при частой записи данных в дыры;
невозможность записи данных в дыры при отсутствии свободного места на диске;
невозможность использования других индикаторов дыр, кроме нулевых байт.

2. ## Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

Нет не могут поскольку "жесткие ссылки" по факту ссылаются на один inode , а поскольку права доступа к объекту ФС хранятся в битовом поле индексного дескриптора (inode) то и права у "жесткой ссылки" будут ровно такие же как и у оригинального файла.


3. ## Сделайте vagrant destroy на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:
```
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.provider :virtualbox do |vb|
    lvm_experiments_disk0_path = "/tmp/lvm_experiments_disk0.vmdk"
    lvm_experiments_disk1_path = "/tmp/lvm_experiments_disk1.vmdk"
    vb.customize ['createmedium', '--filename', lvm_experiments_disk0_path, '--size', 2560]
    vb.customize ['createmedium', '--filename', lvm_experiments_disk1_path, '--size', 2560]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk0_path]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk1_path]
  end
end
```
## Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.
Виртуальная машина создана.

4. ## Используя fdisk, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.
В данный момент в системе несколько дисков
```
Disk /dev/sda: 64 GiB, 68719476736 bytes, 134217728 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B4F1CD46-1589-455C-BA21-5171874A019C

Device       Start       End   Sectors Size Type
/dev/sda1     2048      4095      2048   1M BIOS boot
/dev/sda2     4096   2101247   2097152   1G Linux filesystem
/dev/sda3  2101248 134215679 132114432  63G Linux filesystem


Disk /dev/sdb: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 31.51 GiB, 33822867456 bytes, 66060288 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```
Создаем 2 раздела на диске /dev/sdb
```
root@vagrant:~# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xe72a56cf.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (1-4, default 1): 1
First sector (2048-5242879, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-5242879, default 5242879): +2G

Created a new partition 1 of type 'Linux' and of size 2 GiB.

Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (2-4, default 2): 2
First sector (4196352-5242879, default 4196352):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (4196352-5242879, default 5242879):

Created a new partition 2 of type 'Linux' and of size 511 MiB.

Command (m for help): wq
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

5. ## Используя sfdisk, перенесите данную таблицу разделов на второй диск.
```
root@vagrant:~# sfdisk -d /dev/sdb | sfdisk /dev/sdc
Checking that no-one is using this disk right now ... OK

Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Created a new DOS disklabel with disk identifier 0xe72a56cf.
/dev/sdc1: Created a new partition 1 of type 'Linux' and of size 2 GiB.
/dev/sdc2: Created a new partition 2 of type 'Linux' and of size 511 MiB.
/dev/sdc3: Done.

New situation:
Disklabel type: dos
Disk identifier: 0xe72a56cf

Device     Boot   Start     End Sectors  Size Id Type
/dev/sdc1          2048 4196351 4194304    2G 83 Linux
/dev/sdc2       4196352 5242879 1046528  511M 83 Linux

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```
Переечитываем таблицу разделов
``
partprobe
``

6. ## Соберите mdadm RAID1 на паре разделов 2 Гб.
Собираем RAID1 из разделов /dev/sdb1 и /dev/sdc1
```
root@vagrant:~# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sdb1 /dev/sdc1
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
mdadm: size set to 2094080K
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
root@vagrant:~# fdisk -l /dev/md0
Disk /dev/md0: 1.102 GiB, 2144337920 bytes, 4188160 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

7. ## Соберите mdadm RAID0 на второй паре маленьких разделов.
```
root@vagrant:~# mdadm --create --verbose /dev/md1 -l 0 -n 2 /dev/sdb2 /dev/sdc2
mdadm: chunk size defaults to 512K
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md1 started.
root@vagrant:~# fdisk -l /dev/md1
Disk /dev/md1: 1018 MiB, 1067450368 bytes, 2084864 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 524288 bytes / 1048576 bytes.
```

8. ## Создайте 2 независимых PV на получившихся md-устройствах.
```
root@vagrant:~# pvcreate  /dev/md0
  Physical volume "/dev/md0" successfully created.
root@vagrant:~# pvcreate  /dev/md1
  Physical volume "/dev/md1" successfully created.
```
Физический уровень LVM сейчас выглядит так
```
root@vagrant:~# pvdisplay
  --- Physical volume ---
  PV Name               /dev/sda3
  VG Name               ubuntu-vg
  PV Size               <63.00 GiB / not usable 0
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              16127
  Free PE               8063
  Allocated PE          8064
  PV UUID               sDUvKe-EtCc-gKuY-ZXTD-1B1d-eh9Q-XldxLf

  --- Physical volume ---
  PV Name               /dev/md0
  VG Name               vg1
  PV Size               <2.00 GiB / not usable 0
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              511
  Free PE               511
  Allocated PE          0
  PV UUID               cjFlev-sm2G-g9HX-xSTY-P1WF-jZdq-ikkiSc

  --- Physical volume ---
  PV Name               /dev/md1
  VG Name               vg1
  PV Size               1018.00 MiB / not usable 2.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              254
  Free PE               254
  Allocated PE          0
  PV UUID               VATBsB-4r1c-EqOa-10ja-esik-9r0k-a9fJan
  ```
  
9. ## Создайте общую volume-group на этих двух PV.
```
root@vagrant:~# vgcreate vg1 /dev/md0 /dev/md1
  Volume group "vg1" successfully created
```

10. ## Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.
```
root@vagrant:~# lvcreate -L 100M -n lv1 vg1 /dev/md1
  Logical volume "lv1" created.
```

11. ## Создайте mkfs.ext4 ФС на получившемся LV.
```
root@vagrant:~# mkfs.ext4 /dev/vg1/lv1
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done

```

12. ## Смонтируйте этот раздел в любую директорию, например, /tmp/new.
```
root@vagrant:~# mkdir /tmp/new
root@vagrant:~# mount /dev/vg1/lv1 /tmp/new
```

13. ## Поместите туда тестовый файл, например wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz.
```
root@vagrant:~# wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
--2022-05-16 01:44:53--  https://mirror.yandex.ru/ubuntu/ls-lR.gz
Resolving mirror.yandex.ru (mirror.yandex.ru)... 213.180.204.183, 2a02:6b8::183
Connecting to mirror.yandex.ru (mirror.yandex.ru)|213.180.204.183|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 23063684 (22M) [application/octet-stream]
Saving to: ‘/tmp/new/test.gz’

/tmp/new/test.gz                                     100%[====================================================================================================================>]  22.00M  2.95MB/s    in 7.9s

2022-05-16 01:45:01 (2.80 MB/s) - ‘/tmp/new/test.gz’ saved [23063684/23063684]
```

14. ## Прикрепите вывод lsblk.
```
root@vagrant:~# lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55.5M  1 loop  /snap/core18/2344
loop2                       7:2    0 61.9M  1 loop  /snap/core20/1405
loop3                       7:3    0 67.8M  1 loop  /snap/lxd/22753
loop4                       7:4    0 61.9M  1 loop  /snap/core20/1434
loop5                       7:5    0 70.3M  1 loop  /snap/lxd/21029
loop6                       7:6    0 44.7M  1 loop  /snap/snapd/15534
loop7                       7:7    0 55.5M  1 loop  /snap/core18/2409
sda                         8:0    0   64G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0    1G  0 part  /boot
└─sda3                      8:3    0   63G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md0                     9:0    0    2G  0 raid1
└─sdb2                      8:18   0  511M  0 part
  └─md1                     9:1    0 1018M  0 raid0
    └─vg1-lv1             253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2.5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md0                     9:0    0    2G  0 raid1
└─sdc2                      8:34   0  511M  0 part
  └─md1                     9:1    0 1018M  0 raid0
    └─vg1-lv1             253:1    0  100M  0 lvm   /tmp/new
```

15. ## Протестируйте целостность файла:
```
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
Все верно

16. ## Используя pvmove, переместите содержимое PV с RAID0 на RAID1.
```
root@vagrant:~# pvmove -i5 /dev/md1 /dev/md0
  /dev/md1: Moved: 12.00%
  /dev/md1: Moved: 100.00%
```

17. ## Сделайте --fail на устройство в вашем RAID1 md.
```
root@vagrant:~# mdadm --detail /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Sun May 15 23:52:15 2022
        Raid Level : raid1
        Array Size : 2094080 (2045.00 MiB 2144.34 MB)
     Used Dev Size : 2094080 (2045.00 MiB 2144.34 MB)
      Raid Devices : 2
     Total Devices : 2
       Persistence : Superblock is persistent

       Update Time : Tue May 17 22:09:45 2022
             State : clean
    Active Devices : 2
   Working Devices : 2
    Failed Devices : 0
     Spare Devices : 0

Consistency Policy : resync

              Name : vagrant:0  (local to host vagrant)
              UUID : 31b87075:f96ff9c6:7b8d9339:cc0265d5
            Events : 17

    Number   Major   Minor   RaidDevice State
       0       8       17        0      active sync   /dev/sdb1
       1       8       33        1      active sync   /dev/sdc1
root@vagrant:~# mdadm /dev/md0 -f /dev/sdc1
mdadm: set /dev/sdc1 faulty in /dev/md0
root@vagrant:~# mdadm --detail /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Sun May 15 23:52:15 2022
        Raid Level : raid1
        Array Size : 2094080 (2045.00 MiB 2144.34 MB)
     Used Dev Size : 2094080 (2045.00 MiB 2144.34 MB)
      Raid Devices : 2
     Total Devices : 2
       Persistence : Superblock is persistent

       Update Time : Tue May 17 22:14:30 2022
             State : clean, degraded
    Active Devices : 1
   Working Devices : 1
    Failed Devices : 1
     Spare Devices : 0

Consistency Policy : resync

              Name : vagrant:0  (local to host vagrant)
              UUID : 31b87075:f96ff9c6:7b8d9339:cc0265d5
            Events : 19

    Number   Major   Minor   RaidDevice State
       0       8       17        0      active sync   /dev/sdb1
       -       0        0        1      removed

       1       8       33        -      faulty   /dev/sdc1
```

18. ## Подтвердите выводом dmesg, что RAID1 работает в деградированном состоянии.
```
[108104.875277] md/raid1:md0: Disk failure on sdc1, disabling device.
                md/raid1:md0: Operation continuing on 1 devices.
```

19. ## Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:
```
root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0
```
Все верно с файлом все в порядке, поскольку он "де факто" находится на разделе /dev/sdb1
20. ## Погасите тестовый хост, vagrant destroy.

Готово
