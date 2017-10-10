# linux 用户管理

### 一、添加用户 [参考](http://www.cnblogs.com/irisrain/p/4324593.html)

```
# 格式
useradd [-d home] [-s shell] [-c comment] [-m [-k template]] [-f inactive] [-e expire ] [-p passwd] [-r] name

# 主要参数
	-c：加上备注文字，备注文字保存在passwd的备注栏中。
	
　　-d：指定用户登入时的主目录，替换系统默认值/home/<用户名>
　　
　　-D：变更预设值。
　　
　　-e：指定账号的失效日期，日期格式为MM/DD/YY，例如06/30/12。缺省表示永久有效。
　　
　　-f：指定在密码过期后多少天即关闭该账号。如果为0账号立即被停用；如果为-1则账号一直可用。默认值为-1.
　　
　　-g：指定用户所属的群组。值可以使组名也可以是GID。用户组必须已经存在的，期默认值为100，即users。
　　
　　-G：指定用户所属的附加群组。
　　
　　-m：自动建立用户的登入目录。
　　
　　-M：不要自动建立用户的登入目录。
　　
　　-n：取消建立以用户名称为名的群组。
　　
　　-r：建立系统账号。
　　
　　-s：指定用户登入后所使用的shell。默认值为/bin/bash。
　　
　　-u：指定用户ID号。该值在系统中必须是唯一的。0~499默认是保留给系统用户账号使用的，所以该值必须大于499。

# 说明
useradd可用来建立用户账号，它和adduser命令是相同的。账号建好之后，再用passwd设定账号的密码。使用useradd命令所建立的账号，实际上是保存在/etc/passwd文本文件中。

# 新建一个用户 testuser，并设置UID为 544，主目录为 /home/testuser,属于 users 组：
useradd -u 544 -d /home/testuser -g users -m testuser # 加 -m 如果主目录不存在则自动创建
# 设置密码
passwd testuser

# 使用 useradd 时，如果后面不添加任何参数选项，例如：
# #sudo useradd test 创建出来的用户将是默认的“三无”用户：
# 一无 Home Directory，二无密码，三无系统 Shell

# 新创建一个 oracle 用户，这初始化属于 oinstall 组，且同事让他也属于 dba 组。
useradd oracle -g oinstall -G dba

# 无法使用 shell，且其用户目录至 /var/servlet/service
useradd tomcat -d /var/servlet/service -s /sbin.nologin
# 无法使用 shell，且其用户目录至 /var/servlet/service
```

### 二、修改用户 [参考](http://man.linuxde.net/usermod)

```
# 语法
usermid (选项)(参数)

# 选项
	-c<备注>：修改用户帐号的备注文字；
	-d<登入目录>：修改用户登入时的目录；
	-e<有效期限>：修改帐号的有效期限；
	-f<缓冲天数>：修改在密码过期后多少天即关闭该帐号；
	-g<群组>：修改用户所属的群组；
	-G<群组>；修改用户所属的附加群组；
	-l<帐号名称>：修改用户帐号名称；
	-L：锁定用户密码，使密码无效；
	-s：修改用户登入后所使用的shell；
	-u：修改用户ID；
	-U:解除密码锁定。
# 参数
# 登录名：指定要修改信息的用户登录名

# 实例
# 将 newuser2 添加到组 staff 中：
usermod -G staff newuser2
# 修改 newuser 的用户名为 newuser1 ：
usermod -l newuser1 newuser
# 锁定账号 newuser1 ：
usermod -L newuser1
# 解除对 newuser1 的锁定
usermod -U newuser1
```

### 三、删除用户

```
# 删除刚创建的账号 test
userdel test
# 或者连同用户目录一并删除
userdel -f test
# 注意：这里如果用户还在登录的话，会提示，
# 用户正在登录无法删除。
# 此时可能需要强制用户退出。

# 查看当前登录用户的命令：
root@iZbp138x44jlinka2hs6x5Z:/etc/php/7.0/fpm# w
 10:26:05 up 16:55,  1 user,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    *.*.*.*    Mon18    0.00s  0.63s  0.01s sshd: 9988 [priv] 
test     ps1    *.*.*.*    Mon18    0.00s  0.63s  0.01s sshd: 9988 [priv] 

# 这里知道了登录用户的 tty 是 ps1 执行强制退出命令 pkill：
pkill -kill -t ps1
# 执行之后再执行命令 w 可以看到用户已经退出。
# 重复执行第二步的删除用户命令，删除成功。
```

### 四、开启用户 ssh 登录

```
# 进入 passwd 文件， 找到指定的用户吧后面的 /sbin/nologin 改为
/bin/bash
# 保存并关闭
```

### 五、把用户添加到 sudoers

```
# 1.修改 /etc/sudoers 文件，进入超级用户 root，应为没有写权限，
# 所以要先把权限加上
chmod u+w /etc/sudoers
# 2.编辑 /etc/sudoers 文件，找到这一行：root ALL=(ALL:ALL) ALL
# 在下面添加：
user ALL=(ALL:ALL) ALL # 这里 user 是你的用户名
# 3.最后回复没有写权限模式，撤销文件的写权限
chmod u-w /etc/sudoers # 之后就可以使用 sudo user 了
```

### 六、添加 sftp 用户（并设置）

> 查看 linux_setting_ssh.md 文件