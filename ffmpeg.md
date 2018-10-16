# 安装使用 ffmpeg

### 安装

* 1、下载 ffmpeg安装包 下载地址 http://www.ffmpeg.org/download.html
```
wget -c https://ffmpeg.org/releases/ffmpeg-4.0.2.tar.bz2
```
* 2、解压
```
tar -xvjf ffmpeg-4.0.2.tar.bz2
```
* 3、编译安装
```
cd ffmpeg-4.0.2
./configure --enable-shared --prefix=/usr/local/ffmpeg
make
make install
```
* 如果提示 nasm/yasm not found or too old. Use --disable-x86asm for a crippled build.
```
# 安装 yasm
apt-get install yasm
# 之后在使用第3步操作
```

### 使用
```
# ffmpeg获得视频时间长度的Duration的linux命令
ffmpeg -i test.flv 2>&1 | grep 'Duration' | cut -d ' ' -f 4 | sed s/,//
# grep命令：匹配查找文件里符合条件的字符串，这里查找Duration字段
# cut：以空格为分割符，查询第四个元素，cut是很好的切割命令

# 文件创建时间
ffmpeg -i test.flv 2>&1 | grep 'creationdate' | cut -d ' ' -f  5-
# Cut是文本截取命令：以空格作为分隔符，截取第5位以后的字段
# 如果想要截取： 第5个元素和第8个元素，应该这样写：
ffmpeg -i test.flv 2>&1 | grep 'creationdate' | cut -d ' ' -f  5,8

# 获得视频尺寸大小
# 使用cut截取以空格为分隔符的第十个元素也是视频尺寸
ffmpeg -i test.flv 2>&1 | grep 'Video' | cut -d ' ' -f 10 | sed s/,//
# sed命令：sed ‘s/要替换的字符串/新字符串/g'
# 例如：sed s/,//：表示：用空白符替换','号
```