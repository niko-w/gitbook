### 基本命令

#### tail

> tail命令从文件指定点开始将文件写到标准输出流，使用**tail命令的-f选项**可以方便的查阅正在改变的日志文件,`tail -f filename`会把filename里最尾部的内容显示在屏幕上,并且不但刷新,使你看到最新的文件内容.

##### 命令格式

`tail [ -f ] [ -c Number | -n Number | -m Number | -b Number | -k Number ] [ File ]`

###### 参数解释：

-f 该参数用于监视File文件增长。
-c Number 从 Number 字节位置读取指定文件
-n Number 从 Number 行位置读取指定文件。
-m Number 从 Number 多字节字符位置读取指定文件，比方你的文件假设包括中文字，假设指定-c参数，可能导致截断，但使用-m则会避免该问题。
-b Number 从 Number 表示的512字节块位置读取指定文件。
-k Number 从 Number 表示的1KB块位置读取指定文件。
File 指定操作的目标文件名称
上述命令中，都涉及到number，假设不指定，默认显示10行。Number前面可使用正负号，表示该偏移从顶部还是从尾部開始计算。
tail可运行文件一般在\/usr\/bin\/以下。

#### 查看Linux系统内核信息

* 显示电脑及操作系统相关信息
  `uname -a`
* 显示正在运行的内核版本
  `cat /proc/version`
* 显示发行版本信息
  `cat /etc/issue`
* 适用于所有的linux，包括Redhat、SuSE、Debian等发行版，但是在debian下要安装lsb
  `lsb_release -a`
  ![](/assets/QQ截图20161008090405.png)

#### CentOS上安装lsb\_release命令

lsb\_release命令用来查看当前系统的发行版信息（prints certain LSB \(Linux Standard Base\) and Distribution information.）。有了这个命令就可以清楚的知道到底是RedHat的、还是别的发行版，还有具体的版本号，比如3.4还是5.4等等。
**1、查看哪个源包含这个命令**
`yum provides */lsb_release`

```
[root@localhost niko]# yum provides */lsb_release
Loaded plugins: fastestmirror, refresh-packagekit, security
Determining fastest mirrors
 * base: centos.ustc.edu.cn
 * extras: centos.ustc.edu.cn
 * updates: centos.ustc.edu.cn
base                                                                               
extras                                                                             
mariadb                                                                            
updates                                                                            
updates/primary_db                                                                 
updates/filelists_db                                                               
redhat-lsb-core-4.0-7.el6.centos.i686 : LSB base libraries support for CentOS
Repo        : base
Matched from:
Filename    : /usr/bin/lsb_release



redhat-lsb-core-4.0-7.el6.centos.x86_64 : LSB base libraries support for CentOS
Repo        : base
Matched from:
Filename    : /usr/bin/lsb_release


```

**2、安装包含该命令的包**
从上面的输出可以看到redhat-lsb-core-4.0-7.el6.centos.i686和redhat-lsb-core-4.0-7.el6.centos.x86\_64这两个package包含这个命令，那就安装这两个包中的任意一个即可。
`yum install redhat-lsb-core-4.0-7.el6.centos.i686`


**3、测试命令是否安装成功**
`lsb_release -a`

```
[root@localhost niko]# lsb_release -a
LSB Version:    :base-4.0-ia32:base-4.0-noarch:core-4.0-ia32:core-4.0-noarch
Distributor ID:    CentOS
Description:    CentOS release 6.8 (Final)
Release:    6.8
Codename:    Final

```

