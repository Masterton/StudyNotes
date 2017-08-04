# 安装 gitlab 服务器

### Ubuntu 安装 gitlab [官方安装教程](https://about.gitlab.com/installation/#ubuntu)

> 1、Install and configure the necessary dependencies
```
sudo apt-get install curl openssh-server ca-certificates postfix -y
```

> 2、Add the GitLab package server and install the package

```
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt-get install gitlab-ce
```

> 3、Configure and start GitLab

```
sudo gitlab-ctl reconfigure
```

> 4、Browse to the hostname and login

### CentOS 安装 gitlab [官方安装教程](https://about.gitlab.com/installation/#centos-7)