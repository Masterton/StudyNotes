# mysql数据库主从同步

### 一、开启防火墙3306端口

### 二、Master 主服务器配置

### 三、Slave 从服务器配置

### mysql数据库主从同步参数参考

```
server-id = 1
log_bin = master-bin
log_bin_index = master-bin.index
binlog_do_db = my_data
binlog_ignore_db = mysql
```