# linux 用户管理

### 一、添加用户

### 二、修改用户

### 三、删除用户

### 四、开启用户 ssh 登录

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