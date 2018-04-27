# php-redis

### 1、redis 安装

* 1、windows 版本安装

> 1、安装 redis
> a) 首先到 github 网站上下载 redis [下载地址](https://github.com/dmajkic/redis/downloads)
> b) 根据实际情况，将 64bit/32bit 的内容cp到自定义盘符目录，例如 D:\Redis
> c) 打开cmd，进入 D:\Redis 目录，运行 redis-server.exe redis.conf
> d) 这时候另外开启一个cmd窗口，原来的不要关闭，不然就无法访问服务器了。切换到 D:\Redis 目录下运行  redis-cli.exe -h 127.0.0.1 -p 6379 （-a password远端）
> e) 设置键值对 set mykey abc  取键值对 get mykey
> 这时候，windows环境下，redis的服务端和客户端都运行成功了

```
cd D:
cd Redis
redis-server.exe redis.conf
```

```
cd D:
cd Redis
D:\Redis>redis-cli.exe -h 127.0.0.1 -p 6379
redis 127.0.0.1:6379> set mykey abc
OK
redis 127.0.0.1:6379> get mykey
"abc"
redis 127.0.0.1:6379>
```

> 2、安装 php-redis 扩展
> 查看使用的的 PHP 版本（我使用的是php7.0.1）
> 查看 PHP 使用的 Compiler 是 vc几（我使用的是 vc14）
> 查看使用的 PHP Extension 是什么时候的（我的是	20151012）
> 查看 PHP 使用的 Architecture 是多少位的（我的是x86）
> 根据不同的PHP版本情况下载不同的扩展
> php7 igbinary下载（选择对应版本） [下载地址](http://windows.php.net/downloads/pecl/releases/igbinary/) 
> php redis 下载（选择对应版本） [下载地址](https://pecl.php.net/package/redis)
> 下载下来后把 php_igbinary.dll 和 php_redis.dll 解压到对应PHP安装目录下的 ext/ 文件下
> 修改对应 PHP 版本下的 php.ini 文件（在文件最后添加）

```
[redis]
; php_redis
; 这个必须在 redis 之前
extension=php_igbinary.dll
extension=php_redis.dll
```

* 2、linux 版本安装(Ubuntu)

> 到 redis 官网下载 redis（自己选择下载版本） [下载地址](https://redis.io/download)
> 下载源码，解压后编译源码
> 安装成功后，运行 redis 服务，就可以使用（不要关闭）

```
$ wget http://download.redis.io/releases/redis-3.2.9.tar.gz
$ tar xzf redis-3.2.9.tar.gz # tar.gz 文件解压
$ cd redis-3.2.9
$ make

$ src/redis-server # 直接运行服务[设置后台运行redis](http://blog.csdn.net/ksdb0468473/article/details/52126009)

# 后台运行设置，打开redis.conf 找到 daemonize no 改为
daemonize yes

# 另外打开一个终端
[zheng@iZ94fxluii0Z redis-3.2.9]$ src/redis-cli 
127.0.0.1:6379> set foo bar
OK
127.0.0.1:6379> get foo
"bar"
127.0.0.1:6379>
```

> 安装 php-redis 扩展[参考](http://blog.csdn.net/wkupaochuan/article/details/8627304)

```
# 1、在[下载适合自己php版本的php-redis版本](http://pecl.php.net/package/redis)
wget -c http://pecl.php.net/get/redis-4.0.1.tgz
tar xvf redis-4.0.1.tgz # tgz 文件解压
cd redis-4.0.1


# 调用 phpize 程序生成编译配置文件 configure 配置文件
zheng@iZwz9i0q74l7rt467ggyz2Z:~/www/php-redis-3.1.3$ phpize
Configuring for:
PHP Api Version:         20151012
Zend Module Api No:      20151012
Zend Extension Api No:   320151012


# 编译扩展库
# 这里需要特别注意，一定要把用户切换到root权限，只有root权限在下面redis编译安装时才能把redis.so 文件写入php扩展文件夹 /usr/lib/php/20151012
php-config # 查看php-config 的路径是什么
# Usage： 就是 php-config 的路径
# --extension-dir 就是生成的 redis.so 写入php扩展的文件夹

root@iZbp1bdm1m8u064es7jt23Z:~/www/redis-4.0.1# php-config
Usage: /usr/bin/php-config [OPTION]
Options:
  --prefix            [/usr]
  --includes          [-I/usr/include/php/20151012 -I/usr/include/php/20151012/main -I/usr/include/php/20151012/TSRM -I/usr/include/php/20151012/Zend -I/usr/include/php/20151012/ext -I/usr/include/php/20151012/ext/date/lib ]
  --ldflags           [-L/usr/lib/php/20151012  -L/usr/lib/x86_64-linux-gnu]
  --libs              [-lcrypt   -lresolv -lcrypt -lz -lpcre -lrt -lm -ldl -lnsl  -lxml2 -lssl -lcrypto -lcrypt -lcrypt ]
  --extension-dir     [/usr/lib/php/20151012]
  --include-dir       [/usr/include/php/20151012]
  --man-dir           [/usr/share/man]
  --php-binary        [/usr/bin/php7.0]
  --php-sapis         [apache2handler cgi cli fpm ]
  --phpapi            [20151012]
  --configure-options [--includedir=/usr/include --mandir=/usr/share/man --infodir=/usr/share/info --disable-silent-rules --libdir=/usr/lib/x86_64-linux-gnu --libexecdir=/usr/lib/x86_64-linux-gnu --disable-maintainer-mode --disable-dependency-tracking --prefix=/usr --enable-cli --disable-cgi --disable-phpdbg --with-config-file-path=/etc/php/7.0/cli --with-config-file-scan-dir=/etc/php/7.0/cli/conf.d --build=x86_64-linux-gnu --host=x86_64-linux-gnu --config-cache --cache-file=/build/php7.0-Wn7UbP/php7.0-7.0.28/config.cache --libdir=${prefix}/lib/php --libexecdir=${prefix}/lib/php --datadir=${prefix}/share/php/7.0 --program-suffix=7.0 --sysconfdir=/etc --localstatedir=/var --mandir=/usr/share/man --disable-all --disable-debug --disable-rpath --disable-static --with-pic --with-layout=GNU --without-pear --enable-filter --with-openssl=yes --with-pcre-regex=/usr --enable-hash --with-mhash=/usr --enable-libxml --enable-session --with-system-tzdata --with-zlib=/usr --with-zlib-dir=/usr --enable-dtrace --enable-pcntl --with-libedit=shared,/usr build_alias=x86_64-linux-gnu host_alias=x86_64-linux-gnu CFLAGS=-g -O2 -fPIE -fstack-protector-strong -Wformat -Werror=format-security -O2 -Wall -pedantic -fsigned-char -fno-strict-aliasing -g]
  --version           [7.0.28-0ubuntu0.16.04.1]
  --vernum            [70028]


# 把 redis 的配置信息写入 php-config中
./configure --with-php-config=/usr/bin/php-config # php-config 对应的地址


# 之后，使用 make 编译安装
make && make install


# 使用 make-test 测试安装是否成功

# 最后在 php.ini 的最后面加入
[redis]
extension="redis.so"
```

### 2、php-redis 使用

* 1、