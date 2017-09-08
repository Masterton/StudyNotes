# linux crontab 定时任务管理

### 参考资料

> 1、[bolg参考](http://www.cnblogs.com/intval/p/5763929.html)
> 2、[linux私房菜](http://linux.vbird.org/linux_basic/0430cron.php)

### 操作指令

```
# 直接进入编辑
crontab -e # 直接编辑
crontab -l # 查询使用者目前的 crontab 内容
crontab -r # 移除全部的工作
```

### 格式

> minute hour day month week command
> 其中：
> minute： 表示分钟，可以是从0到59之间的任何整数。
> hour：表示小时，可以是从0到23之间的任何整数。
> day：表示日期，可以是从1到31之间的任何整数。
> month：表示月份，可以是从1到12之间的任何整数。
> week：表示星期几，可以是从0到7之间的任何整数，这里的0或7代表星期日。
> command：要执行的命令，可以是系统命令，也可以是自己编写的脚本文件。