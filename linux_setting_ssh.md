# linux下设置sftp连接账号

> 前言： 开发项目客户要求与三方通过sftp交互文件，我方系统部署sftp服务器。考虑安全，计划对提供给三方的用户实现chroot控制

### 1、查看 openssh 版本

```
zheng@iZwz9i:~/www/$ ssh -V
OpenSSH_7.2p2 Ubuntu-4ubuntu2.2, OpenSSL 1.0.2g  1 Mar 2016
```

### 2、创建用户及用户组

```
# 1、需要创建一个用户组，专门用于 sftp 用户
groupadd sftpusers # 我们的用户组是 sftpusers
# 2、创建一个用户 zheng
useradd -s /bin/false -G sftpusers user # 注意这里我们将 zheng 用户的 shell 设置为 /bin/false 使他没有登录 shell 的权限
passwd zheng # 设置 zheng 用户的密码
# 3、编辑 /etc/ssh/sshd_config
# 先备份 sshd_config
cp sshd_config sshd_config.back
# 在 sshd_config 文件中找到 Subsystem 这个配置项
# 把原有的 Subsystem 行注释掉，添加新的配置，如下：
# Subsystem sftp /usr/lib/openssh/sftp-server

Subsystem sftp internal-sftp

Match Group sftpusers # 组的设置
	X11Forwarding no
	AllowTcpForwarding no
	ForceCommand internal-sftp
	ChrootDirectory /webroot # /webroot 文件夹就是用户 sftp 登录的用户目录

Match User zheng # 单个用户设置
	X11Forwarding no
	AllowTcpForwarding no
	ForceCommand internal-sftp
	ChrootDirectory /webroot # /webroot 文件夹就是用户 sftp 登录的用户目录

# 保存并关闭

# 4、修改 zheng 用户所在文件夹的权限，让其属于 root 用户
chown root:root /webroot
# 5、重启 sshd 服务
service sshd restart
# 6、测试用户账号
ssh zheng@localhost # 链接会被拒绝，证明该用户没有 ssh shell 登录的权限
sftp zheng@localhost # 登录后你会发现你的账号无法切换到除自己本身目录之外的地方
```

> PS：
> 1、如果在链接服务器的时候出现下面的提示：
> Write failed: Broken pipe Couldn't read packet: Connection reset by peer 
> 这个问题的原因是ChrootDirectory的权限问题，你设定的目录必须是root用户所有，否则就会出现问题。所以请确保sftp用户根目录的所有人是root,权限是750 或者755。
> 解决：设置user目录为root权限，# chown root:user /webroot     #chmod 750 /webroot
> 2、Sftp用户登录后不能在本目录操作:
> 是因为登录后的目录是root权限，需将sftp账号赋予root权限，操作方法将  /etc/passwd 文件中对应的sftp的用户ID修改为0，这样就可以有权限操作登录后的目录了(还有其他赋予权限方法，ps另行查找)。Eg：zheng:x:503:505::/home/darops:/bin/false  将503改为0