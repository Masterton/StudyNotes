# 设置 swap 交换空间

### 1、查看 linux 系统分区及内存使用情况

```
# 查看磁盘分区情况
root@iZ2zef0roq6e9vu1vy3rmwZ:/# df -m
Filesystem     1M-blocks  Used Available Use% Mounted on
udev                 479     0       479   0% /dev
tmpfs                100     3        97   3% /run
/dev/vda1          40188  5133     32992  14% /
tmpfs                497     0       497   0% /dev/shm
tmpfs                  5     0         5   0% /run/lock
tmpfs                497     0       497   0% /sys/fs/cgroup
tmpfs                100     0       100   0% /run/user/1000

# 查看内存使用情况
root@iZ2zef0roq6e9vu1vy3rmwZ:/# free -m
              total        used        free      shared  buff/cache   available
Mem:            992          36          60           2         894         795
Swap:          3071           0        3071
```

### 2、创建交换空间 swap

```
# 创建swap交换区硬盘存储用的空白文件。(空间为3G)
root@iZ2zef0roq6e9vu1vy3rmwZ:/# /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=3072
3072+0 records in
3072+0 records out
3221225472 bytes (3.2 GB, 3.0 GiB) copied, 55.1881 s, 58.4 MB/s
root@iZ2zef0roq6e9vu1vy3rmwZ:/# /sbin/mkswap /var
var/
# 使用 mkswap 格式化文件为 swap 文件系统
root@iZ2zef0roq6e9vu1vy3rmwZ:/# /sbin/mkswap /var/swap.1 
Setting up swapspace version 1, size = 3 GiB (3221221376 bytes)
no label, UUID=7ca8ef91-01bc-4874-aed6-a950f8494ef6
# 启用刚才创建的 swap 文件
root@iZ2zef0roq6e9vu1vy3rmwZ:/# /sbin/swapon /var/swap.1
swapon: /var/swap.1: insecure permissions 0644, 0600 suggested.

# 如果有必要可以设置开启自动启动 swap 文件交换区 修改/etc/fstab，增加一行
/var/swap.1 swap swap defaults 0 0 # 启动即启动 swap
# 关闭 swap
root@iZ2zef0roq6e9vu1vy3rmwZ:/# /sbin/swapoff /var/swap.1
```

### 3、修改 swap 交换区空间[参考链接](http://blog.csdn.net/a860mhz/article/details/51124153)
```
# 使用 swapoff 关闭交换区
root@iZ2zef0roq6e9vu1vy3rmwZ:/# swapoff /var/swap.1
# 或者用
root@iZ2zef0roq6e9vu1vy3rmwZ:/# swapoff -a
# 用 lvreduce 命令把 swap 分区减小为 1024M
root@iZ2zef0roq6e9vu1vy3rmwZ:/# lvreduce -L -1024M /var/swap.1
# 输入y，确定，看到提示 swap 减小了1GB
# 重新把 /var/swap.1 设置为 swap 分区
root@iZ2zef0roq6e9vu1vy3rmwZ:/# mkswap /var/swap.1
```

### 4、相关参考
> [Linux SWAP 深度解读](http://blog.csdn.net/wh8_2011/article/details/51798407)
> [Swap交换分区概念](https://www.cnblogs.com/kerrycode/p/5246383.html)
> [Linux调整swap大小和swap性能优化](http://blog.csdn.net/a860mhz/article/details/51124153)