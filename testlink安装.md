> Testlink是测试用例管理工具，可以和jira集成
> TestLink 是基于web的测试用例管理系统，主要功能是测试用例的创建、管理和执行，并且还提供了一些简单的统计功能。

###前言
测试管理工具，是指用工具对软件的整个测试输入、执行过程和测试结果进行管理的过程。可以提高回归测试的效率、大幅提升测试时间、测试质量、用例复用、需求覆盖等。

TestLink用于进行测试过程中的管理，通过使用TestLink提供的功能，可以将测试过程从测试需求、测试设计到测试执行完整地管理起来，同时，它还提供了多种测试结果的统计和分析，使我们能够简单地开始测试工作和分析测试结果。而且，TestLink可以关联多种bug跟踪系统，如Bugzilla、mantis和Jira、readme.

TestLink是sourceforge的开放源代码项目之一，是基于PHP开发的、WEB方式的测试管理系统，其功能可以分为两部分――管理和计划执行。

管理部分，包括产品管理、用户管理、测试需求管理和测试用例管理；

计划执行部分，包括测试计划并执行测试计划，最后显示相关的测试结果分析和测试报告。

### window10下搭建Testlink

#### 准备工作

###### 1.下载xampp

[https:\/\/sourceforge.net\/projects\/xampp\/files\/latest\/download](https://sourceforge.net/projects/xampp/files/latest/download)

> XAMPP（Apache+MySQL+PHP+PERL）是一个功能强大的建站集成软件包。这个软件包原来的名字是 LAMPP，但是为了避免误解，最新的几个版本就改名为 XAMPP 了。它可以在Windows、Linux、Solaris、Mac OS X 等多种操作系统下安装使用，支持多语言：英文、简体中文、繁体中文、韩文、俄文、日文等

###### 2.下载testlink-1.9.15.tar.gz

[https:\/\/sourceforge.net\/projects\/testlink\/files\/TestLink%201.9\/TestLink%201.9.15\/testlink-1.9.15.tar.gz\/download](https://sourceforge.net/projects/testlink/files/TestLink%201.9/TestLink%201.9.15/testlink-1.9.15.tar.gz/download)

#### 开始

###### 1.安装xampp

安装后，在安装文件夹中启动xampp-control.exe，然后再弹出的对话框中启动mysql,apache,tomcat等等
![](/assets/QQ截图20160921164926.png)

点击图片中mysql条目后面的Admin,进入如下的界面
![](/assets/QQ截图20160921184745.png)
在这里设置mysql的root用户密码
`UPDATE mysql.user SET password=PASSWORD(900923) WHERE user='root';`
设置完之后，pshAdmin界面无法访问mysql了，此时需要更改D:\xampp\phpMyAdmin\config.inc.php中的内容

```
/* Authentication type and info */
$cfg['Servers'][$i]['auth_type'] = 'config';
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = '900923';//原来这是是空字符，后面改成了刚刚设置的密码，然后就可以访问mysql了
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['AllowNoPassword'] = true;
$cfg['Lang'] = '';
```

###### 2.安装testlink

解压testlink-1.9.15.tar.gz,将解压后的文件夹拷贝到xampp文件夹下面的htdocs文件夹里，然后再浏览器中输入`http://localhost:80/testlink-1.9.15`可以访问testlink
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

然后再新的页面中设置mysql的用户名及密码，其中database admin为刚刚设置的mysql数据库的用户名和密码，testlink db的用户名和密码可以随意设置
![](/assets/QQ截图20160921171844.png)
![](/assets/QQ截图20160921171907.png)
![](/assets/QQ截图20160921171918.png)

安装成功，点击下图的红色部分，访问testlink，用户名和密码均为admin
![](/assets/QQ截图20160921185903.png)

```
<!-- Template jiradbInterface --> 
<issuetracker> 
<username>wangq</username> 
<password>1111</password> 
<uribase>http://113.108.186.130:11009</uribase> 
<uriapi>http://113.108.186.130:11009</uriapi> 
<uriview>http://113.108.186.130:11009/browse</uriview> 
<projectkey>UDAL</projectkey> 
<issuetype>1</issuetype> 
</issuetracker> 
```

