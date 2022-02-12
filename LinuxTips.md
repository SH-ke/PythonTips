# $Linux$ 相关操作笔记

## 01. $ Linux $ 用户相关操作

添加用户 Ubuntu，同时创建家目录 Ubuntu 使用bash窗口

```shell
ssh -L8888:localhost:8888 Couser@39.96.61.230

useradd -d /home/ubuntu -s /bin/bash ubuntu
su ubuntu
```

添加 $sudoers$ 

```shell
root@SH-ke:~# chmod u+w /etc/sudoers
root@SH-ke:~# vim /etc/sudoers
root@SH-ke:~# chmod u-w /etc/sudoers
```



```shell
# See the man page for details on how to write a sudoers file.
#
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root    ALL=(ALL:ALL) ALL
Couser  ALL=(ALL:ALL) ALL # 添加
jupyter ALL=(ALL:ALL) ALL # 添加

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
Couser  ALL=(ALL:ALL) NOPASSWD:ALL # 添加
jupyter ALL=(ALL:ALL) NOPASSWD:ALL # 添加


# See sudoers(5) for more information on "#include" directives:

#includedir /etc/sudoers.d
```

## 02. $Anaconda$

使用 $wget$ 下载 $Anaconda$

```shell
# 下载 推荐清华源
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2021.11-Linux-x86_64.sh
wget https://repo.anaconda.com/archive/Anaconda3-2021.11-Linux-x86_64.sh
# 2021 最新版Anaconda

# 安装
sudo bash Anaconda3-2021.11-Linux-x86_64.sh

# 添加环境变量
# /home/jupyter/.bashrc
# 没有 .bashrc 文件 /etc/skel/.bashrc 保留有原始文件
export PATH=~/anaconda3/bin:$PATH # anaconda3/ 目录所在的地方
# /etc/.profile
export  PATH=/home/jupyter/anaconda3/bin:$PATH # 系统启动时便激活环境，副产品是界面由文字颜色

# 查看文件生效
conda --version
```

## 03. $WordPress$ 搭建简易网站

安装 宝塔控制面板

```shell
wget –O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh
wget -O install.sh http://download.bt.cn/install/install-ubuntu.sh && sudo bash install.sh

==================================================================
Congratulations! Install succeeded!
==================================================================
Bt-Panel: http://39.96.61.230:8888
username: jyh8eaao
password: 18321297
Warning:
If you cannot access the panel,
release the following port (8888|888|80|443|20|21) in the security group
==================================================================

# 修改密码
cd /www/server/panel && python tools.pyc panel 新密码 用户名

# 命令行卸载
/etc/init.d/bt stop && rm-f /etc/init.d/bt && rm-rf /www/server/panel

# sh脚本卸载
# 首先下载卸载脚本
wget http://download.bt.cn/install/bt-uninstall.sh

# 然后登录root权限，停止服务，然后执行卸载脚本
su
service bt stop
sh bt-uninstall.sh
```

安装 $php\;7.1$

判断系统是否内置了add-apt-repository命令，如果没有执行下列命令安装

```shell
sudo apt-get install software-properties-common
```

$git$
安装一下git程序，很多地方会用到

```shell
sudo apt-get install git
```


设置一下自己的$git$名字和邮箱

```shell
git config --global user.name "你的名字或昵称"
git config --global user.email "你的邮箱"
```

$php$
添加最新php的源，然后安装php

```shell
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php7.1 php7.1-common php7.1-fpm php7.1-dev 
sudo apt-get install php7.1-mbstring php7.1-xml
```

安装结束之后就可以执行php -i命令查看到php-cli的信息 



## 04. 进程 后台挂载

