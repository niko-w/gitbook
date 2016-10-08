前提条件：配置好IP，关闭iptables和selinux

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
2、如果要永久关闭，可以修改配置文件/etc/selinux/config，将SELINU置为disabled。


