**前提条件：配置好IP，关闭iptables和selinux**

* 关闭iptables
  `service iptables stop`
* 关闭selinux
  通常情况下，默认selinux是启用状态
  如下所示：
  ```
  [root@localhost niko]# sestatus
  SELinux status:                 enabled
  SELinuxfs mount:                /selinux
  Current mode:                   enforcing
  Mode from config file:          enforcing
  Policy version:                 24
  Policy from config file:        targeted
  ```


1、临时关闭可以执行`setenforce 0`
此时状态入下：

```
[root@localhost niko]# setenforce 0
[root@localhost niko]# sestatus
SELinux status:                 enabled
SELinuxfs mount:                /selinux
Current mode:                   permissive
Mode from config file:          enforcing
Policy version:                 24
Policy from config file:        targeted
```

2、如果要永久关闭，可以修改配置文件\/etc\/selinux\/config，将SELINU置为disabled。

#### 步骤

##### 1、安装Apache

* 查看是否安装了Apache软件
  `rpm -qa|grep httpd`

  ```
  [root@localhost niko]# rpm -qa|grep httpd
  httpd-tools-2.2.15-53.el6.centos.x86_64
  httpd-2.2.15-53.el6.centos.x86_64
  ```

* 启动Apache软件
  `service httpd start`

  ```
  [root@localhost niko]# service httpd start
  Starting httpd: httpd: Could not reliably determine the server's fully qualified domain name, using localhost.localdomain for ServerName
                                                       [  OK  ]
  ```

  在浏览器中输入[http:\/\/虚拟机IP\/](http://虚拟机IP/) 能显示Apahce的欢迎界面


##### 2、追加CentOS 6.5的epel及remi源

```
rpm -Uvh http://mirrors.ustc.edu.cn/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
```

使用yum list命令查看可安装的包\(Packege\)。
`yum list --enablerepo=remi --enablerepo=remi-php56 | grep php`

##### 3、yum源安装好了，下一步配置PHP5.6

```
yum install --enablerepo=remi --enablerepo=remi-php56 php php-opcache php-devel php-mbstring php-mcrypt php-mysqlnd php-phpunit-PHPUnit php-pecl-xdebug php-pecl-xhprof
```

##### 4、查看php版本

```
[root@localhost niko]# php -v
PHP 5.6.26 (cli) (built: Sep 15 2016 14:57:05) 
Copyright (c) 1997-2016 The PHP Group
Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies
    with Xdebug v2.4.1, Copyright (c) 2002-2016, by Derick Rethans
[root@localhost niko]# 

```

##### 5、安装mysql

* 查看是否安装了mysql,没有则安装

```
[root@localhost niko]# rpm -qa|grep mysql
php-mysqlnd-5.6.26-1.el6.remi.x86_64
[root@localhost niko]# yum -y install mysql-server mysql-client
Loaded plugins: fastestmirror, refresh-packagekit, security
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: centos.ustc.edu.cn
 * epel: ftp.riken.jp
 * extras: centos.ustc.edu.cn
 * remi-safe: mirrors.tuna.tsinghua.edu.cn
 * updates: centos.ustc.edu.cn
Package mysql-server-5.1.73-7.el6.x86_64 is obsoleted by MariaDB-server-10.1.16-1.el6.x86_64 which is already installed
Package MariaDB-client-10.1.16-1.el6.x86_64 already installed and latest version
Nothing to do
[root@localhost niko]# rpm -qa|grep mariadb
[root@localhost niko]# rpm -qa|grep MariaDB
MariaDB-compat-10.1.16-1.el6.x86_64
MariaDB-server-10.1.16-1.el6.x86_64
MariaDB-devel-10.1.16-1.el6.x86_64
MariaDB-common-10.1.16-1.el6.x86_64
MariaDB-client-10.1.16-1.el6.x86_64
[root@localhost niko]# mysql -uroot -proot
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 4
Server version: 10.1.16-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> exit
Bye

```

* 由于本系统上安装有MariaDB,所以安装mysql时不成功

##### 5、安装phpMyAdmin

* 解压phpmyadmin
  `tar -zxvf phpMyAdmin-3.5.7-all-languages.tar`
* 将解压后的文件夹改名为phpMyAdmin
* 将phpMyAdmin拷贝到文件夹`/var/www/html`下
  `[root@localhost phpmyadmin]# cp -r phpMyAdmin /var/www/html/`
* 进入到phpMyAdmin文件夹下，执行下列命令
  `[root@localhost phpmyadmin]# cp config.sample.inc.php config.inc.php`
* 修改html文件的权限
  `[root@localhost phpmyadmin]# chmod 777 /var/www/html/`
* 在浏览器中输入 [http:\/\/192.168.27.142\/phpMyAdmin\/](http://192.168.27.142/phpMyAdmin/)
  ![](/assets/QQ截图20161008105136.png)

##### 6、安装testLink

* 解压testLink
  `[root@localhost testlink]# tar -zxvf testlink-1.9.14.tar.gz`
* 将testLink文件夹拷贝到`/var/www/html`文件夹下
  `[root@localhost testlink]# cp -r testlink-1.9.14 /var/www/html/`
* 修改testlink目录下config.inc.php文件中的内容

  ```
  $g_repositoryPath = '/var/testlink/upload_area/';      该路径可默认
  $tlCfg->log_path = '/var/testlink/logs/';              该路径可默认
  $tlCfg->default_language = 'zh_CN';           修改
  $tlCfg->config_check_warning_mode = 'SILENT'; 修改
  ```

* 若上面两个路径没有改动，新建这两个路径：

  ```
  cd /var
  mkdir testlink
  cd testlink
  mkdir logs
  mkdir upload_area
  ```

* 修改这两个目录的权限

  ```
  chmod 777 logs
  chmod 777 upload_area
  cd ..
  chmod -R 777 testlink
  ```

* 重新启动apache服务：service httpd restart

* 安装testlink
  访问[http:\/\/192.168.27.142\/testlink-1.9.14](http://192.168.27.142/testlink-1.9.14)    进入testlink安装页面，点击new installation，

* 设置数据库账号密码\(账号root,密码为之前设置的root\)

* 设置操作testlink数据库的账号和密码\(账号为testlink，密码为testlink\)


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
     安装过程中如果出现如下错误:

    TestLink setup will now attempt to setup the database:
    Creating connection to Database Server:OK!
    Connecting to database `testlink`:OK!
    Creating Testlink DB user `testlink`:OK! (ok - user_exists ok - grant assignment) 
    Processing:sql/mysql/testlink_create_tables.sqlOK!
    Writing configuration file:Failed!

    TestLink couldn't write the config file. Please copy the following into the ../config_db.inc.php file:

    <?php
        // Automatically Generated by TestLink Installer
        define('DB_TYPE', 'mysql');
        define('DB_USER', 'root');
        define('DB_PASS', 'password');
        define('DB_HOST', 'localhost');
        define('DB_NAME', 'testlink');
        define('DB_TABLE_PREFIX', '');
    ?>;

Once that's been done, you can log into TestLink by pointing your browser at your TestLink site.

解决方式:
在testlink目录中创建config\_db.inc.php文件，并拷贝php的代码即可

```
touch config_db.inc.php
vim config_db.inc.php  
```

