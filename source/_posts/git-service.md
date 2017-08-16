---
title: 配置git服务
---

### 目标
搭建Git服务，为了方便团队开发人员代码管理，搭建一个远程免密登录Git Server。

### 环境
aliyun 一台比较干净的 Centos的Linux操作系统。

### 步骤
####  一、为git添加用户

``` bash
# useradd git
``` 

修改 /etc/passwd文件(非必要)
``` bash
git:x:1001:1001::/home/git:/bin/bash
```

改为
``` bash
git:x:1001:1001::/home/git:/bin/sh
```
####  二、安装git
``` bash
# yum install git
```
####  三、安装gitosis
安装 gitosis
``` bash
git clone https://github.com/tv42/gitosis.git
cd gitosis
python setup.py install
```
切换到用户git
初始化 gitosis
``` bash
gitosis-init < /home/git/admin.pub
```
初始化后生成 gitosis-admin.git和gitosis

然后，切换到root 授权
``` bash
chmod 755 /home/git/repositories/gitosis-admin.git/hooks/post-update
```

####  四、创建版本库
创建git版本库
在repositories中创建test.git文件夹
然后初始化版本库 
``` bash
cd test.git
git init --bare
cd ..
chown -R git test.git/
```

### 常见问题

1、python 报错 需要修改默认Python的版本为2.*

2、报错：refusing to merge unrelated histories
加参数 git pull --allow-unrelated-histories

待补充。。。。