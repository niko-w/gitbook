![](/assets/QQ截图20160921171918.png)&gt; Testlink是测试用例管理工具，可以和jira集成

> TestLink 是基于web的测试用例管理系统，主要功能是测试用例的创建、管理和执行，并且还提供了一些简单的统计功能。

### window10下搭建Testlink

#### 准备工作

1.下载xampp
[https:\/\/sourceforge.net\/projects\/xampp\/files\/latest\/download](https://sourceforge.net/projects/xampp/files/latest/download)

> XAMPP（Apache+MySQL+PHP+PERL）是一个功能强大的建站集成软件包。这个软件包原来的名字是 LAMPP，但是为了避免误解，最新的几个版本就改名为 XAMPP 了。它可以在Windows、Linux、Solaris、Mac OS X 等多种操作系统下安装使用，支持多语言：英文、简体中文、繁体中文、韩文、俄文、日文等

2.下载testlink-1.9.15.tar.gz
[https:\/\/sourceforge.net\/projects\/testlink\/files\/TestLink%201.9\/TestLink%201.9.15\/testlink-1.9.15.tar.gz\/download](https://sourceforge.net/projects/testlink/files/TestLink%201.9/TestLink%201.9.15/testlink-1.9.15.tar.gz/download)

#### 开始

1.安装xampp
安装后，在安装文件夹中启动xampp-control.exe，然后再弹出的对话框中启动mysql,apache,tomcat等等
![](/assets/QQ截图20160921164926.png)&gt;

2.解压testlink-1.9.15.tar.gz,将解压后的文件夹拷贝到xampp文件夹下面的htdocs文件夹里，然后再浏览器中输入`http://localhost:80/testlink-1.9.15`可以访问testlink
![](/assets/101527451655203.jpg)
点击**new installation** 弹出如下界面
![](/assets/QQ截图20160921170123.png)
![](/assets/QQ截图20160921170138.png)
![](/assets/QQ截图20160921170238.png)
注意，此步骤报如下错误

```
Checking if /var/testlink/logs/ directory exists [S]    Failed!
Checking if /var/testlink/upload_area/ directory exists [S]    Failed!
```

修改D:\xampp\htdocs\testlink-1.9.15\config.inc.php中的内容

```
//$tlCfg->log_path = '/var/testlink/logs/'; /* unix example */注释掉，修改为如下的内容
$tlCfg->log_path = 'D:/xampp/htdocs/testlink-1.9.15/logs/';
```

```
//$g_repositoryPath = '/var/testlink/upload_area/';  /* unix example */注释掉，修改为如下的内容
$g_repositoryPath = 'D:/xampp/htdocs/testlink-1.9.15/upload_area/';
```

修改完后，重新加载testlink的界面，如下：
![](/assets/QQ截图20160921171703.png)

然后再新的页面中设置mysql的用户名及密码
![](/assets/QQ截图20160921171844.png)
![](/assets/QQ截图20160921171907.png)
![](/assets/QQ截图20160921171918.png)

