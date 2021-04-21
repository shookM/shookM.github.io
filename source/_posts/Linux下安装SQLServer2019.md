---
title: Linux下安装SQLServer2019
tags: [Linux, SQLServer]
index_img: /img/bg/3.jpg #缩略图-a
banner_img: /img/bg/1.jpg #banner图-a
top_img: /img/md/md4.png #banner图-b
cover:  /img/md/md5.jpg #缩略图-b
date: 2021-01-29 13:34
updated: 2021-01-29 13:34

---
**今天有需求需要装一个SQLServer的数据库**

**之前一直在WinServer下装SQLServer，因为一直在体验.NetCore跨平台，虽然手头还有WinServer服务器但还是用Linux装一回SQLServer试试**

### 一、安装环境

**系统环境：CentOS(Rathat)**

**其他环境以及其他信息参考微软官方文档进行查阅：https://docs.microsoft.com/zh-cn/learn/modules/deploy-sql-server-linux/**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8fceb38d2bf0416d8a6c81945fcc48c8~tplv-k3u1fbpfcp-zoom-1.image)

### 二、进行安装

**我们先看下官方的安装流程：https://docs.microsoft.com/zh-cn/learn/modules/deploy-sql-server-linux/7-exercise-install-sql-server-redhat**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b8dce18fbc7e46db8da8a4f001af0d19~tplv-k3u1fbpfcp-zoom-1.image)

**因为使用yum进行安装会出现众所周知的“网络问题”【狗头】**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c5da7fd45ce04322bba445959528a251~tplv-k3u1fbpfcp-zoom-1.image)

**所以我们这里省略了一些流程，使用rpm包离线安装，那么开始进行安装**

**rpm包下载地址：**

**https://packages.microsoft.com/rhel/7/mssql-server-2019/**

**https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-15.0.4083.2-15.x86_64.rpm**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/167b2594c02c490aa645eca4c816e460~tplv-k3u1fbpfcp-zoom-1.image)

**百度云地址（失效的话可以留言）：链接: https://pan.baidu.com/s/1C0LdESwp7E6FvW6tkXtOzg 提取码: eigr**

**安装rpm**

```
[root@aaa local]# rpm  -ivh mssql-server-15.0.4083.2-15.x86_64.rpm
准备中...                          ################################# [100%]
正在升级/安装...
   1:mssql-server-15.0.4083.2-15      ################################# [100%]

+--------------------------------------------------------------+
请运行 "sudo /opt/mssql/bin/mssql-conf setup"
完成 Microsoft SQL Server 的设置
+--------------------------------------------------------------+

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/22826f4857b34740ba28acce402f23a3~tplv-k3u1fbpfcp-zoom-1.image)

**Microsoft SQL Server 的设置，我这里是选择Developer，其他配置根据自己需要进行配置**

```
[root@aaa local]# sudo /opt/mssql/bin/mssql-conf setup
usermod：无改变
选择 SQL Server 的一个版本:
  1) Evaluation (免费，无生产许可，180 天限制)
  2) Developer (免费，无生产许可)
  3) Express (免费)
  4) Web (付费版)
  5) Standard (付费版)
  6) Enterprise (付费版) - CPU 核心利用率限制为 20 个物理/40 个超线程
  7) Enterprise Core (付费版) - CPU 核心利用率达到操作系统最大值
  8) 我通过零售渠道购买了许可证并具有要输入的产品密钥。

可在以下位置找到有关版本的详细信息:
https://go.microsoft.com/fwlink/?LinkId=2109348&clcid=0x804

使用此软件的付费版本需要通过以下途径获取单独授权
Microsoft 批量许可计划。
选择付费版本即表示你具有适用的
要安装和运行此软件的就地许可证数量。

输入版本(1-8): 2
可以在以下位置找到此产品的许可条款:
/usr/share/doc/mssql-server 或从以下位置下载:
https://go.microsoft.com/fwlink/?LinkId=2104294&clcid=0x804

可以从以下位置查看隐私声明:
https://go.microsoft.com/fwlink/?LinkId=853010&clcid=0x804

接受此许可条款吗? [Yes/No]:Yes


选择 SQL Server 的语言:
(1) English
(2) Deutsch
(3) Español
(4) Français
(5) Italiano
(6) 日本語
(7) 한국어
(8) Português
(9) Русский
(10) 中文 – 简体
(11) 中文 （繁体）
输入选项 1-11:10
输入 SQL Server 系统管理员密码:
指定的密码不符合 SQL Server 密码策略要求，因为该密码太短。密码必须至少为 8 个字符
输入 SQL Server 系统管理员密码:
指定的密码不符合 SQL Server 密码策略要求，因为它不够复杂。密码必须至少包含 8 个字符，并包含以下四种字符集中的任意三种: 大写字母、小写字母、数字和符号。
输入 SQL Server 系统管理员密码:
确认 SQL Server 系统管理员密码:
正在配置 SQL Server...

ForceFlush is enabled for this instance.
ForceFlush feature is enabled for log durability.
Created symlink from /etc/systemd/system/multi-user.target.wants/mssql-server.service to /usr/lib/systemd/system/mssql-server.service.
安装程序已成功完成。SQL Server 正在启动。

```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3d63b8cfc6c640e289f17c876cda3e6f~tplv-k3u1fbpfcp-zoom-1.image)



**验证一下SQL Server是否成功启动**

```systemctl status mssql-server --no-pager```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c52b944839544d079aaed7cc0c74b811~tplv-k3u1fbpfcp-zoom-1.image)

**查看下端口**
```[root@ayc local]# netstat -ntlp```

**我们这里不使用linux的命令在Linux链接sqlserver，使用Navicat等工具进行连接测试一下**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a7880fec064648d7a81634613c922a0b~tplv-k3u1fbpfcp-zoom-1.image)

**到此Linux下的安装就ok**

**如果Docker下有需求的可以看一下官方文档：https://docs.microsoft.com/zh-cn/learn/modules/run-sql-server-2017-linux-containers/**

**这里先不做过多演示，以后再有安装需求会更新Docker的安装过程**
