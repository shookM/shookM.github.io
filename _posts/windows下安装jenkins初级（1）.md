## 这里是基于Windows系统下安装Jenkins

首先下载jenkins

下载地址：[https://jenkins.io/download/](http://www.shookm.com/wp-content/themes/begin/inc/go.php?url=https://jenkins.io/download/)

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214161120-1-1024x469.png)

选择所需要的系统 我这里选择Windows

开始安装

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20181214161742.png)

一直Next就ok

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214155547-1024x565.png)

浏览器会自动跳转 window的带时间会长一些

默认的端口为8080，后面可以更改，不过笔者之前实验会发生BUG

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214162057-1024x707.png)

等待结束会弹出上面的页面

C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword

我们去这个位置去查看首次登陆需要的密码，我这里安装选择的位置是C:\Program Files (x86) 所以去这里找一哈

这里我们安装插件，我们选择默认安装插件

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214163122-1024x574.png)

等待安装就可以啦

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214163355-1024x671.png)

安装完毕，这里我们出现了部分插件安装错误

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214165142-1024x707.png)

点击继续，会输入你要设置的账号及密码

这里会让你选择端口，我这里选择默认

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214165330-1024x718.png)

进入之后我们选择系统管理

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214165722-1024x517.png)

我这里报了之前插件的错误

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214165820-1024x447.png)

我们在插件管理中选择高级

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214165946.png)

在最下面我们找到两个选项，第一个可以自行下载插件自行安装，自由度高，稳定一点

插件地址：

[https://updates.jenkins.io/download/plugins/](http://www.shookm.com/wp-content/themes/begin/inc/go.php?url=https://updates.jenkins.io/download/plugins/)

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181214170058-1024x402.png)

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217095921-2-1024x737.png)

第二个我们可以选择国内提供的站点来下载

https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json

也可以去网上搜一下站点

不过我们这里选择默认+安装插件的方式

我们这里已经更新完毕

![jenkins初级-安装](http://www.shookm.com/wp-content/uploads/2018/12/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20181217111122-1024x536.png)