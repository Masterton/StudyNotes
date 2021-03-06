# Ubuntu 配置服务器环境

### 配置LAMP

> 1、更新 apt 包

```
sudo apt-get update
```

> 2、安装 ssh 服务供外部用 xshell 连接服务器

```
# 查看是否有安装SSH服务
ps -e | grep ssh*
# 如果没有任何显示，则安装该服务
# 安装 openssh-server
sudo apt-get install openssh-server
# 安装 openssh-client
sudo apt-get install openssh-client
# 查看安装SSH服务成功与否
ps -e | grep sshd # 查询sshd服务
zheng@zheng-virtual-machine:/$ ps -e | grep sshd
  4322 ?        00:00:00 sshd
  4385 ?        00:00:00 sshd
  4464 ?        00:00:00 sshd
# 如果看见sshd表明ssh-server启动了，否则
/etc/init.d/ssh start # 启动服务
# 查看ssh默认配置(默认服务端口是22)
root@ubuntu:/etc/ssh# more ssh_config

# ubuntu20.04版本高了之后，使用ssh连接服务器报错

vim /etc/ssh/sshd_config

# 把下面这句加入到末尾，重启ssh-server服务就可以了
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1
```

> 3、安装 apache2

```
sudo apt-get install apache2
```

> 4、安装php

```
# 查看安装的包
dpkg -l | grep php # 查看安装的php包
dpkg -l # 查看安装的所有包
apt-cache search php7.0 # 查看php7.0的安装包有那些
# 安装php7.0 和扩展
sudo apt-get install php7.0 php7.0-fpm php7.0-gd php7.0-curl php7.0-mysql php7.0-pdo php7.0-mcrypt php7.0-mbstring php7.0-common php7.0-ldap php7.0-cli php7.0-dev php7.0-json
# 安装php7.4 和扩展
apt-get install php7.4 php7.4-fpm php7.4-gd php7.4-curl php7.4-mysql php7.4-pdo php7.4-mbstring php7.4-common php7.4-ldap php7.4-cli php7.4-dev php7.4-json
# 注意：此时是无法解析PHP网页的，因为没有安装apache php module
apt-get install libapache2-mod-php7.0
```

> 5、安装mysql

```
# 安装mysql-server
apt install mysql-server mysql-client
# 设置数据库
# 设置远程连接mysql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;
# 重载授权表：
FLUSH PRIVILEGES;
# 卸载mysql及依赖
apt purge mysql-*

# 重新设置密码，解决不用密码也能登录
use mysql;
update user set authentication_string=PASSWORD("密码") where user='root';
update user set plugin="mysql_native_password";
flush privileges;
quit;
systemctl restart mysql.service;

# 导入slq.gz文件
gunzip < dbname.gz | mysql -u Username -p dbname
gzip -d < aaa.sql.gz | mysql -uroot -p aaa

# 新版mysql8.0 group 报错
# 找到 [mysqld]，在下一行加上下面的内容
[mysqld]
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION


# 最新安装的 mysql8.0 安装的时候没有设置密码的
# 1.查看密码
sudo cat /etc/mysql/debian.cnf

root@iZbp18lo7swichwrkdi1w3Z:/# cat /etc/mysql/debian.cnf 
# Automatically generated for Debian scripts. DO NOT TOUCH!
[client]
host     = localhost
user     = debian-sys-maint
password = RONL9BWwzI2DCUlN
socket   = /var/run/mysqld/mysqld.sock
[mysql_upgrade]
host     = localhost
user     = debian-sys-maint
password = RONL9BWwzI2DCUlN
socket   = /var/run/mysqld/mysqld.sock

# 2.利用 debian-sys-maint 账户登录Mysql
mysql -udebian-sys-maint -p

# 3.查看user表信息：
use mysql;
select user,host,authentication_string from user;

mysql> select user,host,authentication_string from user;
+------------------+-----------+------------------------------------------------------------------------+
| user             | host      | authentication_string                                                  |
+------------------+-----------+------------------------------------------------------------------------+
| debian-sys-maint | localhost | $A$005$(,r_ECkBpFj+4Dq\IewpEHTM/84kaYf77inQP3eNzcrwfvHlJwxHBOGggHr6 |
| mysql.infoschema | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| mysql.session    | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| mysql.sys        | localhost | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED |
| root             | localhost |                                                                        |
+------------------+-----------+------------------------------------------------------------------------+
5 rows in set (0.00 sec)

# 可以明显看到，root账户存在但密码为空。

# 4、修改密码：
alter user 'root'@'localhost' identified with mysql_native_password by 'mysql'; # 修改密码为 mysql
flush privileges; # 重新加载权限表

# 5、退出mysql重新登录
quit;
mysql -uroot -p
```

> 6、开启需要的端口

```
# 开启外部访问端口8080
netstat -anp 查看端口使用情况
# 打开端口
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
# 查看防火墙状态
ufw status
# 防火墙版本
ufw version
# 安装 防火墙
apt-get install ufw
# 启动
ufw enable
ufw default deny # 设置开机启动
# 开启/禁用端口
ufw allow|deny 8080
#开启/关闭防火墙
ufw enable/disable
```

```
# 安装最新的node.js
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```

> 新建linux用户并赋予sudo权限

```
# 在root用户下新建用户
adduser zheng
# 修改/etc/sudoers文件，进入超级用户，因为没有写权限，所以要先把写权限加上
chmod u+w /etc/sudoers
vim /etc/sudoers
# 找到这一 行："root ALL=(ALL) ALL"在起下面添加"
zhc ALL=(ALL) ALL # (这里的zhc是你的用户名)，然后保存。
# 最后恢复没有写权限模式，撤销文件的写权限
chmod u-w /etc/sudoers
```

```
apache目录结构
├── apache2.conf #apache住配置文件
├── conf-available
├── conf-enabled #允许的配置项
├── envvars
├── magic
├── mods-available
├── mods-enabled #允许apache加载的模块
├── ports.conf #apache开启的端口文件
├── sites-available
└── sites-enabled #允许访问的配置
```

```
# ubuntu lamp环境搭建
apt-get install mysql-server \
    mysql-client \
    libssl-dev \
    gcc \
    g++ \
    php7.0 \
    php-dev \
    apache2 \
    libapache2-mod-php7.0 \
    php7.0-fpm \
    php-pear \
    php7.0-common \
    php7.0-gd \
    php7.0-zip \
    php7.0-mysql \
    php7.0-mbstring \
    php7.0-xml \
    php7.0-mcrypt \
    git \
    openssh-client \
    openssh-server

# 启用rewrite模块
a2enmod rewrite
a2enmod expires

# apache 基本命令
service apache2 start	#开启apache
service apache2 stop	#停止apache
service apache2 restart #重启apache
```

```
git cloen 仓库地址 本地的文件夹 	#克隆仓库
git diff 文件路径	#对比文件内容
git branch 分支名	#创建分支
git commit	#提交到本地仓库
git push	#提交到远程仓库
git merge 分支	#合并分支
git fetch 分支	#更新
git pull 分支	#拉取文件到本地
```

```
netstat -apn 查看端口占用详情
service mysql start 启动服务
service mysql stop 停止服务
service mysq restart 重启服务
service mysql status 查看运行状态
ps -aux | grep nginx 查看nginx进程
```

```
apt-get remove php5 卸载php5
dpkg --get-selections|grep php 查看安装的php扩展apt-cache search package 搜索软件包
apt-cache show package  获取包的相关信息，如说明、大小、版本等
sudo apt-get install package 安装包
sudo apt-get install package --reinstall   重新安装包
sudo apt-get -f install   修复安装
sudo apt-get remove package 删除包
sudo apt-get remove package --purge 删除包，包括配置文件等
sudo apt-get update  更新源
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
apt-cache depends package 了解使用该包依赖那些包
apt-cache rdepends package 查看该包被哪些包依赖
sudo apt-get build-dep package 安装相关的编译环境
apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get check 检查是否有损坏的依赖
```

```
# dpkg 命令用法 （Debian package）
dpkg -l package 显示包版本
dpkg -r package 移除软件（保留配置）
dpkg -P package 移除软件（不保留配置）
dpkg -s package 查找包的详细信息
dpkg -c package.deb 列出 deb 包的内容
dpkg -l | grep php 查看安装的包
```

```
apt-cache search # ------(package 搜索包)
apt-cache show #------(package 获取包的相关信息，如说明、大小、版本等)
apt-get install # ------(package 安装包)
apt-get install # -----(package --reinstall 重新安装包)
apt-get -f install # -----(强制安装, "-f = --fix-missing"当是修复安装吧...)
apt-get remove #-----(package 删除包)
apt-get remove --purge # ------(package 删除包，包括删除配置文件等)
apt-get autoremove --purge # ----(package 删除包及其依赖的软件包+配置文件等（只对6.10有效，强烈推荐）)
apt-get update #------更新源
apt-get upgrade #------更新已安装的包
apt-get dist-upgrade # ---------升级系统
apt-get dselect-upgrade #------使用 dselect 升级
apt-cache depends #-------(package 了解使用依赖)
apt-cache rdepends # ------(package 了解某个具体的依赖,当是查看该包被哪些包依赖吧...)
apt-get build-dep # ------(package 安装相关的编译环境)
apt-get source #------(package 下载该包的源代码)
apt-get clean && apt-get autoclean # --------清理下载文件的存档 && 只清理过时的包
apt-get check #-------检查是否有损坏的依赖
dpkg -S filename -----查找filename属于哪个软件包
apt-file search filename -----查找filename属于哪个软件包
apt-file list packagename -----列出软件包的内容
apt-file update --更新apt-file的数据库

dpkg --info "软件包名" --列出软件包解包后的包名称.
dpkg -l --列出当前系统中所有的包.可以和参数less一起使用在分屏查看. (类似于rpm -qa)
dpkg -l |grep -i "软件包名" --查看系统中与"软件包名"相关联的包.
dpkg -s 查询已安装的包的详细信息.
dpkg -L 查询系统中已安装的软件包所安装的位置. (类似于rpm -ql)
dpkg -S 查询系统中某个文件属于哪个软件包. (类似于rpm -qf)
dpkg -I 查询deb包的详细信息,在一个软件包下载到本地之后看看用不用安装(看一下呗).
dpkg -i 手动安装软件包(这个命令并不能解决软件包之前的依赖性问题),如果在安装某一个软件包的时候遇到了软件依赖的问题,可以用apt-get -f install在解决信赖性这个问题.
dpkg -r 卸载软件包.不是完全的卸载,它的配置文件还存在.
dpkg -P 全部卸载(但是还是不能解决软件包的依赖性的问题)
dpkg -reconfigure 重新配置
```

### 配置LNMP
