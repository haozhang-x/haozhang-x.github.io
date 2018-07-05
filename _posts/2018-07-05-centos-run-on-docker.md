---
layout: post
title: centos-run-on-docker     
subtitle:  在docker上运行centos
date: 2018-07-05 22:50:51       
author: 张浩
header-img: "img/post-bg-2015.jpg"
catelog: true
tags:
---

# Docker上运行CentOS
先拉取CentOS的镜像
`docker pull centos`
![docker-pull](../img/in-post/centos-run-on-docker/docker-pull.png)
如遇到速度比较慢的情况可用[**DaoCloud加速器**](https://www.daocloud.io/mirror#accelerator-doc)
![dao-cloud](../img/in-post/centos-run-on-docker/dao-cloud.png)
然后基于CentOS的镜像创建一个容器
`docker run -it centos`
![docker-run](../img/in-post/centos-run-on-docker/docker-run.png)
修改root的密码
`passwd root`
![passwd-root](../img/in-post/centos-run-on-docker/passwd-root.png)
Ctrl+D退出，然后提交本次对容器的更改，生成新的镜像
`docker commit 9e1d0b757ffe mycentos:latest`
![docker-commit](../img/in-post/centos-run-on-docker/docker-commit.png)
然后接着运行生成的新的镜像mycentos:latest
`docker run --cap-add=SYS_ADMIN -ti -e  "container=docker" -v /sys/fs/cgroup:/sys/fs/cgroup mycentos:latest  /usr/sbin/init`
![docker-run-centos](../img/in-post/centos-run-on-docker/docker-run-centos.png)
输入用户root，输入通过passwd root修改的密码
![centos-login](../img/in-post/centos-run-on-docker/centos-login.png)










