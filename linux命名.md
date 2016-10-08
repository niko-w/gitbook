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
1、查看哪个源包含这个命令
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
2、安装包含该命令的包
从上面的输出可以看到redhat-lsb-core-4.0-7.el6.centos.i686和redhat-lsb-core-4.0-7.el6.centos.x86_64这两个package包含这个命令，那就安装这两个包中的任意一个即可。
`yum install redhat-lsb-core-4.0-7.el6.centos.i686`
```
[root@localhost niko]# yum install redhat-lsb-core-4.0-7.el6.centos.i686
Loaded plugins: fastestmirror, refresh-packagekit, security
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: centos.ustc.edu.cn
 * extras: centos.ustc.edu.cn
 * updates: centos.ustc.edu.cn
Resolving Dependencies
--> Running transaction check
---> Package redhat-lsb-core.i686 0:4.0-7.el6.centos will be installed
--> Processing Dependency: perl-Test-Simple for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: perl-Test-Harness for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: perl-ExtUtils-MakeMaker for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: perl-CGI for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libz.so.1 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libutil.so.1 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libstdc++.so.6 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libssl3.so for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: librt.so.1 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libpthread.so.0 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libpam.so.0 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libnss3.so for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libnspr4.so for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libncurses.so.5 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libm.so.6 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libgcc_s.so.1 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libdl.so.2 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libcrypt.so.1 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: libc.so.6 for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: /usr/bin/pax for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: /usr/bin/msgfmt for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Processing Dependency: /bin/gettext for package: redhat-lsb-core-4.0-7.el6.centos.i686
--> Running transaction check
---> Package gettext.x86_64 0:0.17-18.el6 will be installed
--> Processing Dependency: cvs for package: gettext-0.17-18.el6.x86_64
---> Package glibc.i686 0:2.12-1.192.el6 will be installed
--> Processing Dependency: libfreebl3.so(NSSRAWHASH_3.12.3) for package: glibc-2.12-1.192.el6.i686
--> Processing Dependency: libfreebl3.so for package: glibc-2.12-1.192.el6.i686
---> Package libgcc.i686 0:4.4.7-17.el6 will be installed
---> Package libstdc++.i686 0:4.4.7-17.el6 will be installed
---> Package ncurses-libs.i686 0:5.7-4.20090207.el6 will be installed
---> Package nspr.i686 0:4.11.0-1.el6 will be installed
---> Package nss.i686 0:3.21.0-8.el6 will be installed
--> Processing Dependency: nss-softokn(x86-32) >= 3.14.3-22 for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libsoftokn3.so for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.21) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.17.1) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.15) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.14) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.13) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.12.5) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.12.3) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so(NSSUTIL_3.12) for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssutil3.so for package: nss-3.21.0-8.el6.i686
--> Processing Dependency: libnssdbm3.so for package: nss-3.21.0-8.el6.i686
---> Package pam.i686 0:1.1.1-22.el6 will be installed
--> Processing Dependency: libselinux.so.1 for package: pam-1.1.1-22.el6.i686
--> Processing Dependency: libdb-4.7.so for package: pam-1.1.1-22.el6.i686
--> Processing Dependency: libcrack.so.2 for package: pam-1.1.1-22.el6.i686
--> Processing Dependency: libaudit.so.1 for package: pam-1.1.1-22.el6.i686
---> Package pax.x86_64 0:3.4-10.1.el6 will be installed
---> Package perl-CGI.x86_64 0:3.51-141.el6_7.1 will be installed
---> Package perl-ExtUtils-MakeMaker.x86_64 0:6.55-141.el6_7.1 will be installed
--> Processing Dependency: perl-devel for package: perl-ExtUtils-MakeMaker-6.55-141.el6_7.1.x86_64
---> Package perl-Test-Harness.x86_64 0:3.17-141.el6_7.1 will be installed
---> Package perl-Test-Simple.x86_64 0:0.92-141.el6_7.1 will be installed
---> Package zlib.i686 0:1.2.3-29.el6 will be installed
--> Running transaction check
---> Package audit-libs.i686 0:2.4.5-3.el6 will be installed
---> Package cracklib.i686 0:2.8.16-4.el6 will be installed
---> Package cvs.x86_64 0:1.11.23-16.el6 will be installed
---> Package db4.i686 0:4.7.25-20.el6_7 will be installed
---> Package libselinux.i686 0:2.0.94-7.el6 will be installed
---> Package nss-softokn.x86_64 0:3.14.3-23.el6_7 will be updated
---> Package nss-softokn.i686 0:3.14.3-23.3.el6_8 will be installed
--> Processing Dependency: libsqlite3.so.0 for package: nss-softokn-3.14.3-23.3.el6_8.i686
---> Package nss-softokn.x86_64 0:3.14.3-23.3.el6_8 will be an update
---> Package nss-softokn-freebl.x86_64 0:3.14.3-23.el6_7 will be updated
---> Package nss-softokn-freebl.i686 0:3.14.3-23.3.el6_8 will be installed
---> Package nss-softokn-freebl.x86_64 0:3.14.3-23.3.el6_8 will be an update
---> Package nss-util.i686 0:3.21.0-2.el6 will be installed
---> Package perl-devel.x86_64 4:5.10.1-141.el6_7.1 will be installed
--> Processing Dependency: perl(ExtUtils::ParseXS) for package: 4:perl-devel-5.10.1-141.el6_7.1.x86_64
--> Processing Dependency: gdbm-devel for package: 4:perl-devel-5.10.1-141.el6_7.1.x86_64
--> Processing Dependency: db4-devel for package: 4:perl-devel-5.10.1-141.el6_7.1.x86_64
--> Running transaction check
---> Package db4-devel.x86_64 0:4.7.25-20.el6_7 will be installed
--> Processing Dependency: db4-cxx = 4.7.25-20.el6_7 for package: db4-devel-4.7.25-20.el6_7.x86_64
--> Processing Dependency: libdb_cxx-4.7.so()(64bit) for package: db4-devel-4.7.25-20.el6_7.x86_64
---> Package gdbm-devel.x86_64 0:1.8.0-39.el6 will be installed
---> Package perl-ExtUtils-ParseXS.x86_64 1:2.2003.0-141.el6_7.1 will be installed
---> Package sqlite.i686 0:3.6.20-1.el6_7.2 will be installed
--> Processing Dependency: libreadline.so.6 for package: sqlite-3.6.20-1.el6_7.2.i686
--> Running transaction check
---> Package db4-cxx.x86_64 0:4.7.25-20.el6_7 will be installed
---> Package readline.i686 0:6.0-4.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

==================================================================================
 Package                    Arch      Version                    Repository  Size
==================================================================================
Installing:
 redhat-lsb-core            i686      4.0-7.el6.centos           base        25 k
Installing for dependencies:
 audit-libs                 i686      2.4.5-3.el6                base        75 k
 cracklib                   i686      2.8.16-4.el6               base        70 k
 cvs                        x86_64    1.11.23-16.el6             base       712 k
 db4                        i686      4.7.25-20.el6_7            base       580 k
 db4-cxx                    x86_64    4.7.25-20.el6_7            base       588 k
 db4-devel                  x86_64    4.7.25-20.el6_7            base       6.6 M
 gdbm-devel                 x86_64    1.8.0-39.el6               base        26 k
 gettext                    x86_64    0.17-18.el6                base       1.8 M
 glibc                      i686      2.12-1.192.el6             base       4.4 M
 libgcc                     i686      4.4.7-17.el6               base       114 k
 libselinux                 i686      2.0.94-7.el6               base       109 k
 libstdc++                  i686      4.4.7-17.el6               base       302 k
 ncurses-libs               i686      5.7-4.20090207.el6         base       249 k
 nspr                       i686      4.11.0-1.el6               base       116 k
 nss                        i686      3.21.0-8.el6               base       861 k
 nss-softokn                i686      3.14.3-23.3.el6_8          updates    270 k
 nss-softokn-freebl         i686      3.14.3-23.3.el6_8          updates    157 k
 nss-util                   i686      3.21.0-2.el6               base        67 k
 pam                        i686      1.1.1-22.el6               base       658 k
 pax                        x86_64    3.4-10.1.el6               base        69 k
 perl-CGI                   x86_64    3.51-141.el6_7.1           base       209 k
 perl-ExtUtils-MakeMaker    x86_64    6.55-141.el6_7.1           base       294 k
 perl-ExtUtils-ParseXS      x86_64    1:2.2003.0-141.el6_7.1     base        46 k
 perl-Test-Harness          x86_64    3.17-141.el6_7.1           base       232 k
 perl-Test-Simple           x86_64    0.92-141.el6_7.1           base       113 k
 perl-devel                 x86_64    4:5.10.1-141.el6_7.1       base       424 k
 readline                   i686      6.0-4.el6                  base       176 k
 sqlite                     i686      3.6.20-1.el6_7.2           base       306 k
 zlib                       i686      1.2.3-29.el6               base        73 k
Updating for dependencies:
 nss-softokn                x86_64    3.14.3-23.3.el6_8          updates    262 k
 nss-softokn-freebl         x86_64    3.14.3-23.3.el6_8          updates    168 k

Transaction Summary
==================================================================================
Install      30 Package(s)
Upgrade       2 Package(s)

Total download size: 20 M
Is this ok [y/N]: y
Downloading Packages:
(1/32): audit-libs-2.4.5-3.el6.i686.rpm                    |  75 kB     00:00     
(2/32): cracklib-2.8.16-4.el6.i686.rpm                     |  70 kB     00:00     
(3/32): cvs-1.11.23-16.el6.x86_64.rpm                      | 712 kB     00:02     
(4/32): db4-4.7.25-20.el6_7.i686.rpm                       | 580 kB     00:01     
(5/32): db4-cxx-4.7.25-20.el6_7.x86_64.rpm                 | 588 kB     00:01     
(6/32): db4-devel-4.7.25-20.el6_7.x86_64.rpm               | 6.6 MB     00:11     
(7/32): gdbm-devel-1.8.0-39.el6.x86_64.rpm                 |  26 kB     00:00     
(8/32): gettext-0.17-18.el6.x86_64.rpm                     | 1.8 MB     00:03     
(9/32): glibc-2.12-1.192.el6.i686.rpm                      | 4.4 MB     00:09     
(10/32): libgcc-4.4.7-17.el6.i686.rpm                      | 114 kB     00:00     
(11/32): libselinux-2.0.94-7.el6.i686.rpm                  | 109 kB     00:00     
(12/32): libstdc++-4.4.7-17.el6.i686.rpm                   | 302 kB     00:00     
(13/32): ncurses-libs-5.7-4.20090207.el6.i686.rpm          | 249 kB     00:00     
(14/32): nspr-4.11.0-1.el6.i686.rpm                        | 116 kB     00:00     
(15/32): nss-3.21.0-8.el6.i686.rpm                         | 861 kB     00:01     
(16/32): nss-softokn-3.14.3-23.3.el6_8.i686.rpm            | 270 kB     00:00     
(17/32): nss-softokn-3.14.3-23.3.el6_8.x86_64.rpm          | 262 kB     00:00     
(18/32): nss-softokn-freebl-3.14.3-23.3.el6_8.i686.rpm     | 157 kB     00:00     
(19/32): nss-softokn-freebl-3.14.3-23.3.el6_8.x86_64.rpm   | 168 kB     00:00     
(20/32): nss-util-3.21.0-2.el6.i686.rpm                    |  67 kB     00:00     
(21/32): pam-1.1.1-22.el6.i686.rpm                         | 658 kB     00:01     
(22/32): pax-3.4-10.1.el6.x86_64.rpm                       |  69 kB     00:00     
(23/32): perl-CGI-3.51-141.el6_7.1.x86_64.rpm              | 209 kB     00:00     
(24/32): perl-ExtUtils-MakeMaker-6.55-141.el6_7.1.x86_64.r | 294 kB     00:00     
(25/32): perl-ExtUtils-ParseXS-2.2003.0-141.el6_7.1.x86_64 |  46 kB     00:00     
(26/32): perl-Test-Harness-3.17-141.el6_7.1.x86_64.rpm     | 232 kB     00:00     
(27/32): perl-Test-Simple-0.92-141.el6_7.1.x86_64.rpm      | 113 kB     00:00     
(28/32): perl-devel-5.10.1-141.el6_7.1.x86_64.rpm          | 424 kB     00:00     
(29/32): readline-6.0-4.el6.i686.rpm                       | 176 kB     00:00     
(30/32): redhat-lsb-core-4.0-7.el6.centos.i686.rpm         |  25 kB     00:00     
(31/32): sqlite-3.6.20-1.el6_7.2.i686.rpm                  | 306 kB     00:00     
(32/32): zlib-1.2.3-29.el6.i686.rpm                        |  73 kB     00:00     
----------------------------------------------------------------------------------
Total                                             502 kB/s |  20 MB     00:40     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : libgcc-4.4.7-17.el6.i686                                      1/34 
  Installing : perl-CGI-3.51-141.el6_7.1.x86_64                              2/34 
  Installing : gdbm-devel-1.8.0-39.el6.x86_64                                3/34 
  Installing : glibc-2.12-1.192.el6.i686                                     4/34 
  Installing : nss-softokn-freebl-3.14.3-23.3.el6_8.i686                     5/34 
  Installing : pax-3.4-10.1.el6.x86_64                                       6/34 
  Installing : db4-cxx-4.7.25-20.el6_7.x86_64                                7/34 
  Updating   : nss-softokn-freebl-3.14.3-23.3.el6_8.x86_64                   8/34 
  Installing : cvs-1.11.23-16.el6.x86_64                                     9/34 
  Installing : nspr-4.11.0-1.el6.i686                                       10/34 
  Installing : nss-util-3.21.0-2.el6.i686                                   11/34 
  Installing : db4-4.7.25-20.el6_7.i686                                     12/34 
  Installing : zlib-1.2.3-29.el6.i686                                       13/34 
  Installing : ncurses-libs-5.7-4.20090207.el6.i686                         14/34 
  Installing : db4-devel-4.7.25-20.el6_7.x86_64                             15/34 
  Installing : 1:perl-ExtUtils-ParseXS-2.2003.0-141.el6_7.1.x86_64          16/34 
  Installing : perl-ExtUtils-MakeMaker-6.55-141.el6_7.1.x86_64              17/34 
  Installing : 4:perl-devel-5.10.1-141.el6_7.1.x86_64                       18/34 
  Installing : perl-Test-Harness-3.17-141.el6_7.1.x86_64                    19/34 
  Installing : perl-Test-Simple-0.92-141.el6_7.1.x86_64                     20/34 
  Installing : gettext-0.17-18.el6.x86_64                                   21/34 
  Installing : readline-6.0-4.el6.i686                                      22/34 
  Installing : sqlite-3.6.20-1.el6_7.2.i686                                 23/34 
  Installing : nss-softokn-3.14.3-23.3.el6_8.i686                           24/34 
  Installing : nss-3.21.0-8.el6.i686                                        25/34 
  Installing : libselinux-2.0.94-7.el6.i686                                 26/34 
  Installing : libstdc++-4.4.7-17.el6.i686                                  27/34 
  Installing : cracklib-2.8.16-4.el6.i686                                   28/34 
  Installing : audit-libs-2.4.5-3.el6.i686                                  29/34 
  Updating   : nss-softokn-3.14.3-23.3.el6_8.x86_64                         30/34 
  Installing : pam-1.1.1-22.el6.i686                                        31/34 
  Installing : redhat-lsb-core-4.0-7.el6.centos.i686                        32/34 
  Cleanup    : nss-softokn-3.14.3-23.el6_7.x86_64                           33/34 
  Cleanup    : nss-softokn-freebl-3.14.3-23.el6_7.x86_64                    34/34 
  Verifying  : db4-devel-4.7.25-20.el6_7.x86_64                              1/34 
  Verifying  : nss-3.21.0-8.el6.i686                                         2/34 
  Verifying  : 4:perl-devel-5.10.1-141.el6_7.1.x86_64                        3/34 
  Verifying  : pax-3.4-10.1.el6.x86_64                                       4/34 
  Verifying  : nss-softokn-freebl-3.14.3-23.3.el6_8.i686                     5/34 
  Verifying  : db4-cxx-4.7.25-20.el6_7.x86_64                                6/34 
  Verifying  : pam-1.1.1-22.el6.i686                                         7/34 
  Verifying  : db4-4.7.25-20.el6_7.i686                                      8/34 
  Verifying  : libselinux-2.0.94-7.el6.i686                                  9/34 
  Verifying  : zlib-1.2.3-29.el6.i686                                       10/34 
  Verifying  : libgcc-4.4.7-17.el6.i686                                     11/34 
  Verifying  : glibc-2.12-1.192.el6.i686                                    12/34 
  Verifying  : readline-6.0-4.el6.i686                                      13/34 
  Verifying  : sqlite-3.6.20-1.el6_7.2.i686                                 14/34 
  Verifying  : perl-Test-Simple-0.92-141.el6_7.1.x86_64                     15/34 
  Verifying  : libstdc++-4.4.7-17.el6.i686                                  16/34 
  Verifying  : 1:perl-ExtUtils-ParseXS-2.2003.0-141.el6_7.1.x86_64          17/34 
  Verifying  : gdbm-devel-1.8.0-39.el6.x86_64                               18/34 
  Verifying  : nspr-4.11.0-1.el6.i686                                       19/34 
  Verifying  : cracklib-2.8.16-4.el6.i686                                   20/34 
  Verifying  : perl-CGI-3.51-141.el6_7.1.x86_64                             21/34 
  Verifying  : gettext-0.17-18.el6.x86_64                                   22/34 
  Verifying  : redhat-lsb-core-4.0-7.el6.centos.i686                        23/34 
  Verifying  : perl-ExtUtils-MakeMaker-6.55-141.el6_7.1.x86_64              24/34 
  Verifying  : audit-libs-2.4.5-3.el6.i686                                  25/34 
  Verifying  : perl-Test-Harness-3.17-141.el6_7.1.x86_64                    26/34 
  Verifying  : ncurses-libs-5.7-4.20090207.el6.i686                         27/34 
  Verifying  : nss-softokn-3.14.3-23.3.el6_8.x86_64                         28/34 
  Verifying  : nss-softokn-freebl-3.14.3-23.3.el6_8.x86_64                  29/34 
  Verifying  : cvs-1.11.23-16.el6.x86_64                                    30/34 
  Verifying  : nss-softokn-3.14.3-23.3.el6_8.i686                           31/34 
  Verifying  : nss-util-3.21.0-2.el6.i686                                   32/34 
  Verifying  : nss-softokn-3.14.3-23.el6_7.x86_64                           33/34 
  Verifying  : nss-softokn-freebl-3.14.3-23.el6_7.x86_64                    34/34 

Installed:
  redhat-lsb-core.i686 0:4.0-7.el6.centos                                         

Dependency Installed:
  audit-libs.i686 0:2.4.5-3.el6                                                   
  cracklib.i686 0:2.8.16-4.el6                                                    
  cvs.x86_64 0:1.11.23-16.el6                                                     
  db4.i686 0:4.7.25-20.el6_7                                                      
  db4-cxx.x86_64 0:4.7.25-20.el6_7                                                
  db4-devel.x86_64 0:4.7.25-20.el6_7                                              
  gdbm-devel.x86_64 0:1.8.0-39.el6                                                
  gettext.x86_64 0:0.17-18.el6                                                    
  glibc.i686 0:2.12-1.192.el6                                                     
  libgcc.i686 0:4.4.7-17.el6                                                      
  libselinux.i686 0:2.0.94-7.el6                                                  
  libstdc++.i686 0:4.4.7-17.el6                                                   
  ncurses-libs.i686 0:5.7-4.20090207.el6                                          
  nspr.i686 0:4.11.0-1.el6                                                        
  nss.i686 0:3.21.0-8.el6                                                         
  nss-softokn.i686 0:3.14.3-23.3.el6_8                                            
  nss-softokn-freebl.i686 0:3.14.3-23.3.el6_8                                     
  nss-util.i686 0:3.21.0-2.el6                                                    
  pam.i686 0:1.1.1-22.el6                                                         
  pax.x86_64 0:3.4-10.1.el6                                                       
  perl-CGI.x86_64 0:3.51-141.el6_7.1                                              
  perl-ExtUtils-MakeMaker.x86_64 0:6.55-141.el6_7.1                               
  perl-ExtUtils-ParseXS.x86_64 1:2.2003.0-141.el6_7.1                             
  perl-Test-Harness.x86_64 0:3.17-141.el6_7.1                                     
  perl-Test-Simple.x86_64 0:0.92-141.el6_7.1                                      
  perl-devel.x86_64 4:5.10.1-141.el6_7.1                                          
  readline.i686 0:6.0-4.el6                                                       
  sqlite.i686 0:3.6.20-1.el6_7.2                                                  
  zlib.i686 0:1.2.3-29.el6                                                        

Dependency Updated:
  nss-softokn.x86_64 0:3.14.3-23.3.el6_8                                          
  nss-softokn-freebl.x86_64 0:3.14.3-23.3.el6_8                                   

Complete!

```

3、测试命令是否安装成功
`lsb_release -a`
```
[root@localhost niko]# lsb_release -a
LSB Version:	:base-4.0-ia32:base-4.0-noarch:core-4.0-ia32:core-4.0-noarch
Distributor ID:	CentOS
Description:	CentOS release 6.8 (Final)
Release:	6.8
Codename:	Final

```