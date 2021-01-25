---
title: socket
top: false
cover: false
toc: true
mathjax: true
date: 2020-09-23 08:53:02
password:
summary:
tags:
- 计算机网络
- 通信协议
categories:
- 笔记
typora-copy-images-to: ./socket
---

## 5.Socket

<img src="E:\CodeProject\Hexo\source\_posts\socket\image-20200526115917010.png" alt="img" style="zoom:80%;" />

<img src="E:\CodeProject\Hexo\source\_posts\socket\image-20200527221256700.png" alt="img" style="zoom:80%;" />

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200529102321353.png" alt="image-20200526115917010" style="zoom: 47%;" />

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200529104537723.png" alt="image-20200527221256700" style="zoom: 100%;" />

### 1.快速入门

#### 1.1 网络编程介绍

1. 从大的方面说就是对信息的发送到接受

2. 通过操作相应API调度计算机硬件资源，并利用传输管道（网线）进行数据交换的过程

   <img src="socket\image-20200529102429313.png" alt="image-20200528095825188" style="zoom: 67%;" />

   <img src="\socket\image-20200528095825188.png" alt="image-20200529102321353"  />

   <img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200529105115076.png" alt="image-20200529102429313"  />

#### 1.2 Socket与TCP、UDP

> 什么是Socket

- Socket简单来说是IP地址与端口的结合协议，一种地址和端口的结合描述协议

 （Socket就是对TCP、UDP的一个封装）

- TCP/IP协议的相关API的总称，是网络API的集合实现
- 涵盖了：Stream Socket / Datagram Socket

<img src="https://gitee.com/lastlight/MyPictrue/raw/master/img/image-20200529105224361.png" alt="image-20200529104537723" style="zoom:80%;" />

<img src="E:\CodeProject\Hexo\source\_posts\socket\image-20200529104600350.png" alt="image-20200529104600350" style="zoom:80%;" />

