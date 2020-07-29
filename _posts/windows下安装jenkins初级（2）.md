 

## 这里是基于gitlab拉取代码

 

 

gitlab暂时先不多介绍

 

 

我们需要把git和gitlab连接起来方便拉取代码

 

 

所以需要git的ssh公匙和私匙

 

 

首先在  https://git-scm.com/ 下载git

 

 

安装完毕之后我们会发现右键会多出两个选项 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217133253.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217133253.png)

 

 

 

我们打开Git Bash Here 命令界面 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217133647.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217133647.png)

 

 

 

输入以下命令

 

 

ssh-keygen -t rsa -P '' "

 

 

![此图像的alt属性为空；文件名为微信截图_20181217134201.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217134201.png)

 

 

 

获得公匙和私匙 存放在C:\Users\Administrator\.ssh 下

 

 

我们到这个下面去查看

 

 

![此图像的alt属性为空；文件名为微信截图_20181217134740.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217134740.png)

 

 

 

id_rsa.pub为公匙 我们把公匙放在gitlab项目设置-仓库-部署秘钥

 

 

![此图像的alt属性为空；文件名为微信截图_20181217135400.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217135400.png)

 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217140209-1024x553.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217140209-1024x553.png)

 

 

 


id_rsa为私匙  然后我们把私匙放在jenkins系统管理-凭据-系统-全局凭证-添加私匙

 

 

![此图像的alt属性为空；文件名为微信截图_20181217141351.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217141351.png)

 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217141527-1024x505.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217141527-1024x505.png)

 

 

 

名字随便填 这里我们点确定

 

 

接下来去jenkins下的系统管理-系统设置下的Gitlab填上如下信息

 

 

没有选项的去插件下下载gitlab的插件，svn同理

 

 

![此图像的alt属性为空；文件名为微信截图_20181217151540.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217151540.png)

 

 

 

点击应用保存

 

 

然后再系统设置下的全局工具中修改JDK信息和Git信息

 

 

按照自己的信息填入就可以

 

 

点击应用保存

 

 

![此图像的alt属性为空；文件名为微信截图_20181217155430-1024x517.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217155430-1024x517.png)

 

 

 

我们开始在jenkins上新建一个项目 命名为：Developer

 

 

![此图像的alt属性为空；文件名为微信截图_20181217142545-1024x556.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217142545-1024x556.png)

 

 

 

构建一个自由风格的软件项目 点击确定

 

 

![此图像的alt属性为空；文件名为微信截图_20181217171225.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217171225.png)

 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217171906.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217171906.png)

 

 

 

![此图像的alt属性为空；文件名为微信截图_20181217171832.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217171832.png)

 

gitlab上ssh的地址

 

 

![此图像的alt属性为空；文件名为微信截图_20181217172603.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217172603.png)

 

选择构建触发器，有网址说明之前的步骤没有问题，点击此项

 

 

点击高级

 

 

![此图像的alt属性为空；文件名为微信截图_20181217173034.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217173034.png)

 

点击Generate获得token

 

 

![此图像的alt属性为空；文件名为微信截图_20181217174405-1024x611.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217174405-1024x611.png)

 

 

 

点击应用保存

 

 

我们来测试一下是否成功

 

 

点击push

 

 

![此图像的alt属性为空；文件名为微信截图_20181217174742.png](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217174742.png)

 

 

 

点击push events

 

 

![此图像的alt属性为空；文件名为image-1-1024x63.png](http://www.shookm.com/wp-content/uploads/2018/12/image-1-1024x63.png)

 

 

 

200则成功

 

 

![此图像的alt属性为空；文件名为image-2-1024x566.png](http://www.shookm.com/wp-content/uploads/2018/12/image-2-1024x566.png)