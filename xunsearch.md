# 安装和使用

* 官网【http://www.xunsearch.com/】
* 下载链接【http://www.xunsearch.com/site/download】
* 安装教程【http://www.xunsearch.com/doc/php/guide/start.installation】

### 一、安装
```
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng# wget http://www.xunsearch.com/download/xunsearch-full-latest.tar.bz2
--2018-12-20 14:05:23--  http://www.xunsearch.com/download/xunsearch-full-latest.tar.bz2
Resolving www.xunsearch.com (www.xunsearch.com)... 202.75.216.233
Connecting to www.xunsearch.com (www.xunsearch.com)|202.75.216.233|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10302627 (9.8M) [text/plain]
Saving to: ‘xunsearch-full-latest.tar.bz2’

xunsearch-full-latest.tar.b 100%[=========================================>]   9.83M  10.3MB/s    in 1.0s    

2018-12-20 14:05:24 (10.3 MB/s) - ‘xunsearch-full-latest.tar.bz2’ saved [10302627/10302627]

root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng# ll
total 55012
drwxr-xr-x  7 zheng zheng     4096 Dec 20 14:05 ./
drwxr-xr-x  5 root       root           4096 Aug 12 15:12 ../
-rw-r--r--  1 root       root       10302627 Nov 16 19:22 xunsearch-full-latest.tar.bz2
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng# tar -xjf xunsearch-full-latest.tar.bz2 
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng# ll
total 55016
drwxr-xr-x  8 zheng zheng     4096 Dec 20 14:05 ./
drwxr-xr-x  5 root       root           4096 Aug 12 15:12 ../
drwxr-xr-x  3        501 staff          4096 Nov 16 19:16 xunsearch-full-1.4.12/
-rw-r--r--  1 root       root       10302627 Nov 16 19:22 xunsearch-full-latest.tar.bz2
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng# cd xunsearch-full-1.4.12/
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng/xunsearch-full-1.4.12# ll
total 40
drwxr-xr-x 3        501 staff       4096 Nov 16 19:16 ./
drwxr-xr-x 8 zheng zheng  4096 Dec 20 14:05 ../
-rw-r--r-- 1        501 staff        120 Dec 31  2016 ._.DS_Store
-rw-r--r-- 1        501 staff       6148 Dec 31  2016 .DS_Store
drwxr-xr-x 2        501 staff       4096 Nov 16 19:21 packages/
-rw-r--r-- 1        501 staff       2937 Dec  5  2014 README.md
-rwxr-xr-x 1        501 staff      11165 Oct 16 13:10 setup.sh*
root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng/xunsearch-full-1.4.12# sh setup.sh 

+==========================================+
| Welcome to setup xunsearch(full)         |
| 欢迎使用 xunsearch (完整版) 安装程序     |
+------------------------------------------+
| Follow the on-screen instructions please |
| 请按照屏幕上的提示操作以完成安装         |
+==========================================+

Please specify the installation directory
请指定安装目录 (默认为中括号内的值)
[/usr/local/xunsearch]:setup.sh: 111: read: Illegal option -e
[/usr/local/xunsearch]:

Confirm the installation directory
请确认安装目录：/usr/local/xunsearch [Y/n]y

Checking scws ... no
Installing scws (1.2.3) ... 
Extracting scws package ...
Configuring scws ...
Compiling & installing scws ...
Checking scws dict ... no
Extracting scws dict file ... 
Checking libuuid ... no, try to install it
Extracting libuuid package ...
Configuring libuuid ...
Compiling & installing libuuid ...
Checking xapian-core-scws ... no
Installing xapian-core-scws (1.4.9) ... 
Extracting xapian-core-scws package ...
Configuring xapian-core-scws ...
Compiling & installing xapian-core-scws ...
Checking libevent ... no
Installing libevent (2.0.21-stable) ... 
Extracting libevent package ...
Configuring libevent ...
Compiling & installing libevent ...
Extracting xunsearch package (1.4.12) ...
Configuring xunsearch ...
Compiling & installing xunsearch ...
Cleaning ... done

+=================================================+
| Installation completed successfully, Thanks you |
| 安装成功，感谢选择和使用 xunsearch              |
+-------------------------------------------------+
| 说明和注意事项：                                |
| 1. 开启/重新开启 xunsearch 服务程序，命令如下： |
|    /usr/local/xunsearch/bin/xs-ctl.sh restart
|    强烈建议将此命令写入服务器开机脚本中         |
|                                                 |
| 2. 所有的索引数据将被保存在下面这个目录中：     |
|    /usr/local/xunsearch/data
|    如需要转移到其它目录，请使用软链接。         |
|                                                 |
| 3. 您现在就可以在我们提供的开发包(SDK)基础上    |
|    开发您自己的搜索了。                         |
|    目前只支持 PHP 语言，参见下面文档：          |
|    /usr/local/xunsearch/sdk/php/README
+=================================================+

root@iZbp1bdm1m8u064ukgg8zwZ:/home/zheng/xunsearch-full-1.4.12# /usr/local/xunsearch/bin/xs-ctl.sh restart
WARNING: no server[xs-indexd] is running (BIND:127.0.0.1:8383)
INFO: re-starting server[xs-indexd] ... (BIND:127.0.0.1:8383)
WARNING: no server[xs-searchd] is running (BIND:127.0.0.1:8384)
INFO: re-starting server[xs-searchd] ... (BIND:127.0.0.1:8384)
root@iZbp1bdm1m8u064ukgg8zwZ:/home/wolonggang/xunsearch-full-1.4.12#
```

### xunsearch PHP-SDK 使用
```
$xs = new \XS('demo');
$tokenizer = new \XSTokenizerScws;

// 添加分词词典, 支持 TXT/XDB 格式
// $tokenizer = $tokenizer->addDict();

// 获取分词结果
// $tokenizer = $tokenizer->getResult();

// XSTokenizer 接口
// $tokenizer = $tokenizer->getTokens();

// 获取重要词统计结果
// $tokenizer = $tokenizer->getTops();

// 获取 scws 版本号
// $tokenizer = $tokenizer->getVersion();

// 判断是否包含指定词性的词
// $tokenizer = $tokenizer->hasWord();

// 设置字符集
// $tokenizer = $tokenizer->setCharset();

// 设置分词词典, 支持 TXT/XDB 格式
// $tokenizer = $tokenizer->setDict();

// 设置散字二元组合
// $tokenizer = $tokenizer->setDuality();

// 设置忽略标点符号
$tokenizer = $tokenizer->setIgnore();

// 设置复合分词选项
// $tokenizer = $tokenizer->setMulti();

$text = '清华大学怎么样？';
$words1 = $tokenizer->getResult($text, 3);
$words2 = $tokenizer->getTops($text, 3);

print_r("<pre>");
print_r($tokenizer);
print_r($words1);
print_r($words2);
exit;
```

### 安装过程出现的错误

* 这是 libevent 与 openssl 版本不兼容导致
* 它们的版本关系是这样的
| libevent    | openssl   |
| :-------    | :-------- |
| 2.1.x       | 1.1       |
| 2.0.x       | 1.0       |

* 有两个选择

> 使用 libevent 2.1.x 版本，这与你本机的 openssl 1.1 匹配，无需任何修改直接编译即可。
> 使用 libevent 2.0.x 版本，你需要安装 openssl 1.0 版本，然后在编译时指定链接版本。

> 下面针对第二种选择做详细说明，这种方法是通用的，适用于编译其他软件时出现版本不兼容问题。

> 首先安装 openssl 1.0 版本，注意需要头文件。你可以选择从源码安装，或使用操作系统的仓库下载安装。
> 这类安装包通常带有 "*-dev" 字样，比如 centos 发行版可能是这样的

```
yum install openssl-devel-1.0xxx
```
> openssl 安装完成后，会有一个 pkgconfig/ 目录，实际路径取决于你上一步的操作，一般位于 /usr/lib 或 /usr/local/lib 下。
> 这里我们假设是 /usr/local/lib/openssl-1.0/pkgconfig/， 你需要将它设置成 PKG_CONFIG_PATH 的环境变量值，如

```
export PKG_CONFIG_PATH=/usr/local/lib/openssl-1.0/pkgconfig/
```

> 切换到 libevent 源码目录，把 openssl 头文件路径，及库文件路径加入 configure 配置变量，如

```
./configure CFLAGS="$(pkg-config --cflags openssl)" LDFLAGS="$(pkg-config --libs openssl)"
```

> 清除原内容，并重新编译即可

```
make clean
make -j8
```

> 修改setup.sh文件，安装libevent是不安装openssl扩展 334 行
```
- ./configure --prefix=$prefix >> ../setup.log 2>&1
+ ./configure --prefix=$prefix --disable-openssl >> ../setup.log 2>&1
```