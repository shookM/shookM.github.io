---
title: Certbot配置Let's Encrypt的https_ssl证书以及过程中出现的问题(2021更新)
tags: [Linux, Certbot]
index_img: /img/bg/3.jpg #缩略图-a
banner_img: /img/bg/1.jpg #banner图-a
top_img: /img/md/md9.png #banner图-b
cover:  /img/md/md1.jpg #缩略图-b
date: 2021-03-05 16:23
updated: 2021-03-05 16:23

---
**今天在.Netcore项目里增加了图片验证码功能，在windows部署下未发现问题，但是在Linux（Centos）下部署却出现了如下问题**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/33f3db49114f433eb8d2cb40d9e9e6cd~tplv-k3u1fbpfcp-zoom-1.image)

**查了下是因为用了System.Drawing.Common类库需要在linux下安装一下libgdiplus来支持图像处理，图片处理，因为我的环境是在Docker环境下，所以去要在容器中增加一下**

**我们在构建的Dockerfile里面增加阿里源以及增加libgdiplus，具体如下**

```
FROM mcr.microsoft.com/dotnet/sdk:5.0

RUN ln -s /lib/x86_64-linux-gnu/libdl-2.24.so /lib/x86_64-linux-gnu/libdl.so
 
RUN echo "deb http://mirrors.aliyun.com/debian wheezy main contrib non-free \
deb-src http://mirrors.aliyun.com/debian wheezy main contrib non-free \
deb http://mirrors.aliyun.com/debian wheezy-updates main contrib non-free \
deb-src http://mirrors.aliyun.com/debian wheezy-updates main contrib non-free \
deb http://mirrors.aliyun.com/debian-security wheezy/updates main contrib non-free \
deb-src http://mirrors.aliyun.com/debian-security wheezy/updates main contrib non-free" > /etc/apt/sources.list
 
RUN apt-get update
RUN apt-get install libgdiplus -y && ln -s libgdiplus.so gdiplus.dll

COPY . /publish

WORKDIR /publish
 
EXPOSE 8801
 
CMD ["dotnet", "Test.dll", "--urls", "http://*:8801"]

```

**然后我们执行一下，出现了以下问题**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8cb2108e011b4114adcfe3686b471e21~tplv-k3u1fbpfcp-zoom-1.image)

```
Step 4/9 : RUN apt-get update
 ---> Running in 9b0f24c74c80
Ign:1 http://mirrors.aliyun.com/debian wheezy InRelease
Err:2 http://mirrors.aliyun.com/debian wheezy Release
  404  Not Found [IP: 111.160.44.225 80]
Reading package lists...
E: The repository 'http://mirrors.aliyun.com/debian wheezy Release' does not have a Release file.
The command '/bin/sh -c apt-get update' returned a non-zero code: 100
Unable to find image 'ladder/devtools:latest' locally
docker: Error response from daemon: pull access denied for ladder/devtools, repository does not exist or may require 'docker login': denied: requested access to the resource is denied.
See 'docker run --help'.

```

**看了下是说好像是说镜像的问题**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2520333b924b411eafbf17d0fa21f22a~tplv-k3u1fbpfcp-zoom-1.image)

**查了一下说是wheezy为debian（Linux发行版）的以前版本，因为Asp.Net Core5.0的docker镜像就是基于debian系统构建的，debian每个版本都有相对应的名字**
- 5是Debian
- 6是squeeze
- 7是wheezy
- 8是jessie
- 9是stretch

**那我们把镜像的系统改为最新的stretch，dockerfile如下**

```
FROM mcr.microsoft.com/dotnet/sdk:5.0

RUN ln -s /lib/x86_64-linux-gnu/libdl-2.24.so /lib/x86_64-linux-gnu/libdl.so
 
RUN echo "deb http://mirrors.aliyun.com/debian stretch main contrib non-free \
deb-src http://mirrors.aliyun.com/debian stretch main contrib non-free \
deb http://mirrors.aliyun.com/debian stretch-updates main contrib non-free \
deb-src http://mirrors.aliyun.com/debian stretch-updates main contrib non-free \
deb http://mirrors.aliyun.com/debian-security stretch/updates main contrib non-free \
deb-src http://mirrors.aliyun.com/debian-security stretch/updates main contrib non-free \
deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib \
deb-src http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib" > /etc/apt/sources.list
 
# RUN apt-get update
# RUN apt-get install -y --allow-unauthenticated libgdiplus libc6-dev libgdiplus libx11-dev && ln -s libgdiplus.so gdiplus.dll
# RUN rm -rf /var/lib/apt/lists/*

RUN apt-get update
RUN apt-get install libgdiplus -y && ln -s libgdiplus.so gdiplus.dll

COPY . /publish
 
WORKDIR /publish
 
EXPOSE 8801
 
CMD ["dotnet", "DevTools.dll", "--urls", "http://*:8801"]
```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/aaeb4cd4254c4ae4905c3ba7e4a4b677~tplv-k3u1fbpfcp-zoom-1.image)

**可以看到已经成功启动，再看下验证码**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ba659cff1a82459e8b030a005696cf24~tplv-k3u1fbpfcp-zoom-1.image)

**已经成功识别了，因为我的图片不涉及中文，有中文的问题可以查看其他文章**
