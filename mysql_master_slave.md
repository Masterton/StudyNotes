# mysql数据库主从同步

### 一、开启防火墙3306端口

* 阿里云服务器直接在控制台开启3306端口外部访问权限
* 命令行下开启外部3306端口访问
```
```

### 二、Master 主服务器配置

* 编辑mysql配置文件
```
# ubuntu 16.04 操作系统
# 找到文件 /etc/mysql/mysql.conf.d/mysqld.cnf
# zai [mysqld] 下面添加
server_id=1
log_bin=master-bin
binlog-do-db=db1
expire_logs_days=2
max_binlog_size=21M
```

* 创建同步账号
```
# 登录mysql
mysql -uroot -p
# 格式：mysql> GRANT REPLICATION SLAVE ON *.* TO '帐号'@'从服务器IP或主机名' IDENTIFIED BY '密码';
grant replication slave on *.* to 'repl'@'%' identified by 'repl';
# 用flush privileges刷新MySQL的系统权限相关表，否则会出现拒绝访问
flush privileges;
```

* 主(master)上查看binlog日志文件，以及坐标
```
mysql> show master status;
+------------------+----------+--------------+------------------+
| File       | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| master-bin.000001 |    70 | db1,db2   |     |
+------------------+----------+--------------+------------------+
1 row in set (0.00 sec)
```

### 三、Slave 从服务器配置

* 编辑mysql配置文件
```
# ubuntu 16.04 操作系统
# 找到文件 /etc/mysql/mysql.conf.d/mysqld.cnf
# zai [mysqld] 下面添加
server_id=2
# log_bin=slave-bin-1 # 使这个数据库成为其他数据的主数据库
# binlog-do-db=db2
# expire_logs_days=2
# max_binlog_size=21M
```

* 从(slave)配置访问信息，开启同步。
```
mysql> change master to master_host='192.168.1.1', master_port=3306, master_user='repl', master_password='repl', master_log_file='master-bin.000001', master_log_pos=70;
Query OK, 0 rows affected, 2 warnings (0.34 sec)

mysql> start slave;
Query OK, 0 rows affected (0.04 sec)

mysql> show slave status \G
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 39.104.90.184
                  Master_User: master
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: master-bin.000002
          Read_Master_Log_Pos: 313657
               Relay_Log_File: iZwz9i0q74l7rt467ggyz2Z-relay-bin.000003
                Relay_Log_Pos: 273
        Relay_Master_Log_File: master-bin.000002
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB: 
          Replicate_Ignore_DB: 
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: 
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 313657
              Relay_Log_Space: 157031
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
  Replicate_Ignore_Server_Ids: 
             Master_Server_Id: 1
                  Master_UUID: 9a305b6c-2666-11e8-8f79-00163e0040f3
             Master_Info_File: /var/lib/mysql/master.info
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL
      Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
           Master_Retry_Count: 86400
                  Master_Bind: 
      Last_IO_Error_Timestamp: 
     Last_SQL_Error_Timestamp: 
               Master_SSL_Crl: 
           Master_SSL_Crlpath: 
           Retrieved_Gtid_Set: 
            Executed_Gtid_Set: 
                Auto_Position: 0
         Replicate_Rewrite_DB: 
                 Channel_Name: 
           Master_TLS_Version: 
1 row in set (0.00 sec)

Master_Log_File # 主库mysql的binlog文件名

Read_Master_Log_Pos # 读取主库mysql的binlog文件的位置

Exec_Master_Log_Pos # 从库执行主库mysql的binlog文件的位置

Seconds_Behind_Master # 从库延迟主库同步的时间单位秒

SQL_Delay # 设置从库服务器相较于主库服务器的延迟同步时间
```

### mysql数据库主从同步参数参考

```
server-id=1 # 服务ID，用于区分服务，范围1~2^32-1
log_bin=master-bin # 日志文件名
log_bin_index=master-bin.index
binlog_do_db=my_data # 需要同步数据库
binlog_ignore_db=mysql # 不需要同步(忽略)数据库

# MySQL 磁盘写入策略以及数据安全性
# 每次事务提交时MySQL都会把log buffer的数据写入log file，并且flush(刷到磁盘)中去
innodb_flush_log_at_trx_commit=1

# 当sync_binlog =N (N>0) ，MySQL 在每写 N次 二进制日志binary log时，
# 会使用fdatasync()函数将它的写二进制日志binary log同步到磁盘中去。
# sync_binlog 的默认值是0，像操作系统刷其他文件的机制一样，
# MySQL不会同步到磁盘中去而是依赖操作系统来刷新binary log。
sync_binlog=1

# mysql复制模式，三种：SBR（基于sql语句复制），
# RBR（基于行的复制），MBR（混合模式复制）
binlog_format=MIXED # 混合模式复制
expire_logs_days=7 # binlog过期清理时间
max_binlog_size=20M # binlog每个日志文件大小
```