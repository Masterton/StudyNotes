# linux挂载磁盘

> df 命令详解

* 语法
```
df(选项)(参数)
```
* 选项
```
-a或--all：包含全部的文件系统；
--block-size=<区块大小>：以指定的区块大小来显示区块数目；
-h或--human-readable：以可读性较高的方式来显示信息；
-H或--si：与-h参数相同，但在计算时是以1000 Bytes为换算单位而非1024 Bytes；
-i或--inodes：显示inode的信息；
-k或--kilobytes：指定区块大小为1024字节；
-l或--local：仅显示本地端的文件系统；
-m或--megabytes：指定区块大小为1048576字节；
--no-sync：在取得磁盘使用信息前，不要执行sync指令，此为预设值；
-P或--portability：使用POSIX的输出格式；
--sync：在取得磁盘使用信息前，先执行sync指令；
-t<文件系统类型>或--type=<文件系统类型>：仅显示指定文件系统类型的磁盘信息；
-T或--print-type：显示文件系统的类型；
-x<文件系统类型>或--exclude-type=<文件系统类型>：不要显示指定文件系统类型的磁盘信息；
--help：显示帮助；
--version：显示版本信息。
```
* 参数
```
文件：指定文件系统上的文件。
```
* 实例
```
# 查看系统磁盘设备，默认是KB为单位：
[root@LinServ-1 ~]# df
文件系统               1K-块        已用     可用 已用% 挂载点
/dev/sda2            146294492  28244432 110498708  21% /
/dev/sda1              1019208     62360    904240   7% /boot
tmpfs                  1032204         0   1032204   0% /dev/shm
/dev/sdb1            2884284108 218826068 2518944764   8% /data1

# 使用-h选项以KB以上的单位来显示，可读性高：
[root@LinServ-1 ~]# df -h
文件系统              容量  已用 可用 已用% 挂载点
/dev/sda2             140G   27G  106G  21% /
/dev/sda1             996M   61M  884M   7% /boot
tmpfs                1009M     0 1009M   0% /dev/shm
/dev/sdb1             2.7T  209G  2.4T   8% /data1

# 查看全部文件系统：
[root@LinServ-1 ~]# df -a
文件系统               1K-块        已用     可用 已用% 挂载点
/dev/sda2            146294492  28244432 110498708  21% /
proc                         0         0         0   -  /proc
sysfs                        0         0         0   -  /sys
devpts                       0         0         0   -  /dev/pts
/dev/sda1              1019208     62360    904240   7% /boot
tmpfs                  1032204         0   1032204   0% /dev/shm
/dev/sdb1            2884284108 218826068 2518944764   8% /data1
none                         0         0         0   -  /proc/sys/fs/binfmt_misc

# linux 查看分区是ext3还是ext4
[root@LinServ-1 ~]# df -hT
```

> fidsk 命令详情

* 语法
```
fdisk(选项)(参数)
```
* 选项
```
-b<分区大小>：指定每个分区的大小；
-l：列出指定的外围设备的分区表状况；
-s<分区编号>：将指定的分区大小输出到标准输出上，单位为区块；
-u：搭配"-l"参数列表，会用分区数目取代柱面数目，来表示每个分区的起始地址；
-v：显示版本信息。
```
* 参数
```
设备文件：指定要进行分区或者显示分区的硬盘设备文件。
```
* 实例
```
# 首先选择要进行操作的磁盘：
[root@localhost ~]# fdisk /dev/sdb

# 输入m列出可以执行的命令：
command (m for help): m
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
# 输入p列出磁盘目前的分区情况：
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1           1        8001   8e  Linux LVM
/dev/sdb2               2          26      200812+  83  Linux

# 输入d然后选择分区，删除现有分区：
Command (m for help): d
Partition number (1-4): 1

Command (m for help): d
Selected partition 2

# 查看分区情况，确认分区已经删除：
Command (m for help): print

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System

Command (m for help):

# 输入n建立新的磁盘分区，首先建立两个主磁盘分区：
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p    //建立主分区
Partition number (1-4): 1  //分区号
First cylinder (1-391, default 1):  //分区起始位置
Using default value 1
last cylinder or +size or +sizeM or +sizeK (1-391, default 391): 100  //分区结束位置，单位为扇区

Command (m for help): n  //再建立一个分区
Command action
   e   extended
   p   primary partition (1-4)
p 
Partition number (1-4): 2  //分区号为2
First cylinder (101-391, default 101):
Using default value 101
Last cylinder or +size or +sizeM or +sizeK (101-391, default 391): +200M  //分区结束位置，单位为M

# 确认分区建立成功：
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux

# 再建立一个逻辑分区：
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
e  //选择扩展分区
Partition number (1-4): 3
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391):
Using default value 391

# 确认扩展分区建立成功：
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended

# 在扩展分区上建立两个逻辑分区：
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l //选择逻辑分区
First cylinder (126-391, default 126):
Using default value 126
Last cylinder or +size or +sizeM or +sizeK (126-391, default 391): +400M    

Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l
First cylinder (176-391, default 176):
Using default value 176
Last cylinder or +size or +sizeM or +sizeK (176-391, default 391):
Using default value 391

# 确认逻辑分区建立成功：
Command (m for help): p

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         100      803218+  83  Linux
/dev/sdb2             101         125      200812+  83  Linux
/dev/sdb3             126         391     2136645    5  Extended
/dev/sdb5             126         175      401593+  83  Linux
/dev/sdb6             176         391     1734988+  83  Linux

Command (m for help):

# 从上面的结果我们可以看到，在硬盘sdb我们建立了2个主分区（sdb1，sdb2），1个扩展分区（sdb3），2个逻辑分区（sdb5，sdb6）
# 注意：主分区和扩展分区的磁盘号位1-4，也就是说最多有4个主分区或者扩展分区，逻辑分区开始的磁盘号为5，因此在这个实验中试没有sdb4的。

# 最后对分区操作进行保存：
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

# 建立好分区之后我们还需要对分区进行格式化才能在系统中使用磁盘。

# 在sdb1上建立ext2分区：
[root@localhost ~]# mkfs.ext2 /dev/sdb1
mke2fs 1.39 (29-May-2006)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
100576 inodes, 200804 blocks
10040 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=209715200
7 block groups
32768 blocks per group, 32768 fragments per group
14368 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840

Writing inode tables: done                           
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 32 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.

# 在sdb6上建立ext3分区：
[root@localhost ~]# mkfs.ext3 /dev/sdb6
mke2fs 1.39 (29-May-2006)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
217280 inodes, 433747 blocks
21687 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=444596224
14 block groups
32768 blocks per group, 32768 fragments per group
15520 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Writing inode tables: done                           
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 32 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
[root@localhost ~]#

# 建立两个目录/oracle和/web，将新建好的两个分区挂载到系统：
[root@localhost ~]# mkdir /oracle
[root@localhost ~]# mkdir /web
[root@localhost ~]# mount /dev/sdb1 /oracle
[root@localhost ~]# mount /dev/sdb6 /web

# 查看分区挂载情况：
[root@localhost ~]# df -h
文件系统              容量  已用 可用 已用% 挂载点
/dev/mapper/VolGroup00-LogVol00
                      6.7G  2.8G  3.6G  44% /
/dev/sda1              99M   12M   82M  13% /boot
tmpfs                 125M     0  125M   0% /dev/shm
/dev/sdb1             773M  808K  733M   1% /oracle
/dev/sdb6             1.7G   35M  1.6G   3% /web

# 如果需要每次开机自动挂载则需要修改/etc/fstab文件，加入两行配置：
[root@localhost ~]# vim /etc/fstab

/dev/VolGroup00/LogVol00 /                       ext3    defaults        1 1
LABEL=/boot             /boot                   ext3    defaults        1 2
tmpfs                   /dev/shm                tmpfs   defaults        0 0
devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
sysfs                   /sys                    sysfs   defaults        0 0
proc                    /proc                   proc    defaults        0 0
/dev/VolGroup00/LogVol01 swap                    swap    defaults        0 0
/dev/sdb1               /oracle                 ext2    defaults        0 0
/dev/sdb6               /web                    ext3    defaults        0 0
```

> mount 命令详情

* 语法
```
mount(选项)(参数)
```
* 选项
```
-V：显示程序版本；
-l：显示已加载的文件系统列表；
-h：显示帮助信息并退出；
-v：冗长模式，输出指令执行的详细信息；
-n：加载没有写入文件“/etc/mtab”中的文件系统；
-r：将文件系统加载为只读模式；
-a：加载文件“/etc/fstab”中描述的所有文件系统。
```
* 参数
```
设备文件名：指定要加载的文件系统对应的设备名；
加载点：指定加载点目录。
```
* 实例
```
mount -t auto /dev/cdrom /mnt/cdrom
mount: mount point /mnt/cdrom does not exist           /mnt/cdrom目录不存在，需要先创建。

cd /mnt
-bash: cd: /mnt: No such file or directory

mkdir -p /mnt/cdrom    创建/mnt/cdrom目录
ls
bin   dev  home    lib         media  mnt  proc  sbin     srv  tmp  var
boot  etc  initrd  lost+found  misc   opt  root  selinux  sys  usr

mount -t auto /dev/cdrom /mnt/cdrom     挂载cdrom
mount: block device /dev/cdrom is write-protected, mounting read-only     挂载成功

ll /mnt/cdrom    查看cdrom里面内容
total 859
dr-xr-xr-x  4 root root   2048 Sep  4  2005 CentOS
-r--r--r--  2 root root   8859 Mar 19  2005 centosdocs-man.css
-r--r--r--  9 root root  18009 Mar  1  2005 GPL
dr-xr-xr-x  2 root root 241664 May  7 02:32 headers
dr-xr-xr-x  4 root root   2048 May  7 02:23 images
dr-xr-xr-x  2 root root   4096 May  7 02:23 isolinux
dr-xr-xr-x  2 root root  18432 May  2 18:50 NOTES
-r--r--r--  2 root root   5443 May  7 01:49 RELEASE-NOTES-en.html
dr-xr-xr-x  2 root root   2048 May  7 02:34 repodata
-r--r--r--  9 root root   1795 Mar  1  2005 rpm-GPG-KEY
-r--r--r--  2 root root   1795 Mar  1  2005 RPM-GPG-KEY-centos4
-r--r--r--  1 root root 571730 May  7 01:39 yumgroups.xml
```