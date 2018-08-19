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
[https://www.centos.org](https://www.centos.org)
2. JDK<br>
jdk-8u181-linux-x64.rpm
可到java.oracle.com下载
3. CDH版本的Hadoop
[CDH5](http://archive.cloudera.com/cdh5/cdh/5/)<br>
[http://archive.cloudera.com/cdh5/cdh/5/hadoop-latest.tar.gz](http://archive.cloudera.com/cdh5/cdh/5/hadoop-latest.tar.gz)<br>


## 开始安装
1. 安装JDK
```
卸载自带的OPENJDK
sudo rpm -e $(rpm -qa|grep jdk|tr "\n" " ")
#安装Oracle JDK
rpm -ivh jdk-8u181-linux-x64.rpm
#配置环境变量
#查看JDK 安装位置
rpm -ql jdk
```
2. 解压配置Hadoop
```
#解压Hadoop
tar -zxvf  hadoop-latest.tar.gz -C /opt/
```
3. 设置软连接
```
ln -s /opt/hadoop-2.6.0-cdh5.15.0 /opt/hadoop
ln -s /opt/hadoop/etc/hadoop  /etc/hadoop
```
4. 设置环境变量Path
```
echo 'export HADOOP_HOME=/opt/hadoop' >> ~/.bash_profile
echo 'export PATH=$HADOOP_HOME/bin:$PATH' >> ~/.bash_profile
#使用source 或者 . 使环境变量生效
source ~/.bash_profile
```
5. 配置本机ssh免登陆
```
ssh-keygen -t rsa
ssh-copy-id  localhost
```
6. 配置core-site.xml与hdfs-site.xml<br>
   <b>a.配置core-site.xml</b>
      <configuration>
          <property>
              <name>fs.defaultFS</name>
              <value>hdfs://localhost:9000</value>
          </property>
      </configuration>
    <b>b.配置hdfs-site.xml</b>
      <configuration>
          <property>
              <name>dfs.replication</name>
              <value>1</value>
          </property>
      </configuration>
7. 格式化Namenode启动NameNode
```
hdfs namenode -format
#启动NameNode守护进程和DataNode守护进程
$HADOOP_HOME/sbin/start-dfs.sh
#浏览NameNode的Web界面
http://localhost:50070/
```
