### 硬件配置

建议内存8G+、CPU 4 cores+、硬盘20G+

MySQL建议分配4G内存、SSO分配1G内存、Work分配2G内存

### 操作系统

建议使用一台全新的服务器，理论上支持所有Linux操作系统，建议使用：

* CentOS 6 x86 64位
* CentOS 7 x86 64位

### 需要2个域名

1、sso.xxxx.com，用于统一认证

2、work.xxxx.com，用于主站

如果你没有注册域名，需要给服务器和你的笔记本系统都配置hosts。

Linux位置/etc/hosts，Windows位置C:\Windows\System32\drivers\etc\hosts

配置内容，例如：

192.168.100.2 sso.bigops.com

192.168.100.2 work.bigops.com

切记设置！切记设置！切记设置！！！否则会报错

### ![](/assets/bug1.png) 关闭SElinux

查看状态

> getenforce

临时关闭

> setenforce 0

永久关闭

> vi /etc/sysconfig/selinux
>
> 将SELINUX=enforcing改为SELINUX=disabled
>
> 需要重启系统

### 关闭防火墙，或者容许访问80端口

centos 6

> chkconfig --level 345 iptables off
>
> service iptables stop

centos 7

> systemctl disable iptables
>
> systemctl stop iptables
>
> systemctl disable firewalld
>
> systemctl stop firewalld

### 优化操作系统

> rm -f /etc/security/limits.d/\*
>
> sed -i '/^\[^\#\].\*/d' /etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tnofile\t\t655360"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\thard\tnofile\t\t655360"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tmemlock\t\tunlimited"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\thard\tmemlock \tunlimited"&gt;&gt;/etc/security/limits.conf
>
> echo -e "\*\t\tsoft\tnproc\t\t655360"&gt;/etc/security/limits.d/90-nproc.conf
>
> echo -e "\*\t\thard\tnproc\t\t655360"&gt;&gt;/etc/security/limits.d/90-nproc.conf



