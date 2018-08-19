---
layout:     post
title: "Hadoop Setting up a Single Node Cluster"      
subtitle: Hadoop 单节点安装  
date: 2018-08-19 21:33:16       
author: 张浩
header-img: "img/post-bg-2015.jpg"
catelog: true
tags:
      -Hadoop
      -BigData
---

# Hadoop 单节点安装

## 环境准备
1. CentOS 7.5<br>
https://www.centos.org/
2. Java<br>
jdk-8u181-linux-x64.rpm<br>
可到java.oracle.com下载
3. CDH版本的Hadoop
[CDH5](http://archive.cloudera.com/cdh5/cdh/5/)<br>
http://archive.cloudera.com/cdh5/cdh/5/hadoop-latest.tar.gz<br>


## 开始安装
1. 解压下载好的hadoop-latest.tar.gz
```
#解压
tar -zxvf hadoop-latest.tar.gz -C /opt/
```
> 安装Java
