# linux 设置成代理服务器(安装squid)

* 1、安装依赖软件

```
root@xct-B360M-D2V:/etc/squid# apt-get install -y gcc openssl
```

* 2、安装 squid

```
# 安装
root@xct-B360M-D2V:/etc/squid# apt-get install squid
# 编辑
root@xct-B360M-D2V:/etc/squid# cd /etc/squid/
root@xct-B360M-D2V:/etc/squid# cp squid.conf squid.conf.bak
root@xct-B360M-D2V:/etc/squid# vim squid.conf
```

> 找到这些代码

```
http_access deny all
# http_port 3128
# cache_dir ufs /var/spool/squid 100 16 256
```

> 改为

```
http_access allow all
http_port 0.0.0.0：3128 # 用 netstat -apn |grep 3128 查看是否是 tcp6 如果是就改为0.0.0.0的否则就只需要一个端口号就行了
cache_dir ufs /var/spool/squid 100 16 256
```

> 测试、初始化、启动 squid

```
# 测试
root@xct-B360M-D2V:/etc/squid# squid -k parse
2016/08/09 13:35:04| Processing Configuration File: /etc/squid/squid.conf (depth 0)
2016/08/09 13:35:04| Processing: acl manager proto cache_object
..............
..............
2016/08/09 13:35:04| Processing: refresh_pattern . 0 20% 4320
2016/08/09 13:35:04| Initializing https proxy context
# 初始化
root@xct-B360M-D2V:/etc/squid# squid -z
# 启动squid
root@xct-B360M-D2V:/etc/squid# /etc/init.d/squid start
[ ok ] Restarting squid (via systemctl): squid.service.
```

* 3、开启 3128 端口

```
root@xct-B360M-D2V:/etc/squid# iptables -I INPUT -p tcp --dport 80 -j ACCEPT
root@xct-B360M-D2V:/etc/squid# iptables-save
```

* 4、编辑 hosts 文件

```
# 加入自己想要的ip域名解析
root@xct-B360M-D2V:/etc/squid# vim /etc/hosts
1.1.1.1 test.com
root@xct-B360M-D2V:/etc/squid# /etc/init.d/networking restart
```

* 查看代理是否生效

```
root@xct-B360M-D2V:/etc/squid# curl -x192.168.22.30:3128 'http://www.51cto.com/images/home/images/logo.jpg' -I
HTTP/1.0 200 OK
Server: Tengine
Date: Sun, 24 May 2015 13:42:43 GMT
Content-Type: image/jpeg
Content-Length: 5309
Last-Modified: Wed, 22 Jan 2014 07:55:12 GMT
Expires: Sun, 31 May 2015 13:42:43 GMT
Cache-Control: max-age=604800
Load-Balancing: web39
Accept-Ranges: bytes
Age: 29661
X-Cache: HIT from yonglinux
X-Cache-Lookup: HIT from yonglinux:3128
Via: 1.0 yonglinux (squid/3.1.10)
Connection: keep-alive
```