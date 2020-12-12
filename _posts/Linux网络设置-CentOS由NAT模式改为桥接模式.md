---
title: Linux网络设置-CentOS由NAT模式改为桥接模式
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-02 19:09:28
password:
summary: 这篇文章主要记录将我们的Linux网络设置由NAT模式改为桥接模式。
tags:
- CentOS
- NAT
- Bridged
categories:
- Linux
---





Linux版本：`CentOS`

CentOS发行版本：`CentOS 8.1`

虚拟机：`VMware`



在前面CentOS 8.1安装教程中关于网络配置我们默认使用的是NAT模式，这篇文章主要记录将我们的Linux网络设置由NAT模式改为桥接模式（Bridged）。



需要安装CentOS的朋友可以可以看这篇文章：



[VMware 安装 CentOS 8.1 完整教程](https://muyiio.com/2020/03/05/vmware-an-zhuang-centos-8-1-wan-zheng-jiao-cheng/)



## 1】NAT与Bridged区别

- **NAT(网络地址转换模式)**

虚拟机要联网得先通过宿主机才能和外面进行通信。



NAT模式下的虚拟系统的TCP/IP配置信息是由VMnet8(NAT)虚拟网络的DHCP服务器提供的，无法进行手工修改，因此虚拟系统也就无法和本局域网中的其他真实主机进行通讯。使得虚拟局域网内的虚拟机在对外访问时，使用的则是宿主机的IP地址，这样从外部网络来  看，只能看到宿主机，完全看不到新建的虚拟局域网。就是虚拟系统会通过宿主机的网络来访问外网，而这里的宿主机相当于有两个网卡，一个是真实网卡，一个是虚拟网卡，真实网卡相当于链接了现实世界的真实路由器，而宿主机的虚拟网卡，相当于连接了一个可以认为是虚拟交换机。



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/1229366-20171112202534434-1791559898.png)



**虚拟机可以上网可以ping通主机，但是主机ping不通虚拟机。**



- **Bridged(桥接模式)**

虚拟机和宿主机在网络上就是平级的关系，相当于连接在同一交换机上。

需要手工为虚拟系统配置IP地址、子网掩码，而且还要和宿主机器处于同一网段，这样虚拟系统才能和宿主机器进行通信。以实现通过局域网的网关或路由器访问互联网。使用bridged模式的虚拟系统和宿主机器的关系，就像连接在同一个Hub上的两台电脑。相当于在一个局域网内创立了一个单独的主机，他可以访问这个局域网内的所有的主机，但是需要手动来配置IP地址，子网掩码，并且他是和真实主机在同一个网段（nat是两个网段）.



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/1229366-20171112203200528-1382297812.png)



**这个模式里，虚拟机和宿主机可以互相ping通。**



## 3】虚拟机网络设置

**右键点击以管理员身份打开VMware，找到要更改网络的虚拟机。**

- 点击左上角【编辑虚拟机设置】→【网络适配器】→选择【桥接模式】，并勾选【复制物理网络连接状】态

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164719.png)



- 点击左上角【编辑E】→【虚拟网络编辑器】

>  VMnet0、VMnet1、VMnet8，分别对应了桥接模式、仅主机模式、NAT模式。





**选择【VMnet0】→【已桥接至】选择当前电脑连接的网络→【确定】**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164729.png)





## 3】CentOS网络设置

- 查看自己电脑的IP网段（Win+R输入cmd再输入ipconfig）



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164945.png)



**将 IPv4 地址、子网掩码 、默认网关保存后面用到。**





- 打开虚拟机，以root账户登录CentOS

1.由于我安装了图形界面，登录是这样：





![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164605.png)

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164629.png)

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164633.png)



说明：**倘若没有设置root账户，但登录的账户yyo拥有root权限，那就直接登陆。**



2.没有安装图形界面登录简单一些，我就不演示了。





- 获取权限

```
sudo -i
```



- 编辑配置ip地址信息文件（使用vi打开，CentOS自带vi）

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```



可以看到我们的网络配置文件：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164646.png)



**按`i`进入编辑，按`方向键`移动**



修改这两个值：

```
BOOTPROTO=static       #设置为手动分配IP地址
ONBOOT=yes
```



在`ONBOOT=yes`后面增加四个值（上面我们保存的ip）：

```
IPADDR=192.168.0.107   # 配置为局域网固定IP(IPv4 地址)
NETMASK=255.255.255.0  # 配置子网掩码
GATEWAY=192.168.0.1    # 配置局域网网关
DNS1=8.8.8.8           # 配置首选DNS，8.8.8.8为免费DNS服务器的IP地址
```



**编辑完成后按`esc`退出，再按`:wq`保存（如果无法保存，就按`:wq！`强制保存）**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164738.png)



- 接下来修改第二个配置，输入下面这个命令

```
vi /etc/sysconfig/network
```



增加这四个配置：

**按`i`进入编辑，按`方向键`移动**

```
NETWORKING=yes
NETWORKING_IPV6=no            #关掉IPv6
HOSTNAME=localhost.localdomain
GATEWAY=192.168.0.1           #默认网关地址
```



**编辑完成后按`esc`退出，再按`:wq`保存**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164800.png)



- 启动network服务,输入下面这个命令

```
service network restart
```



**使用CentOS 8.x 版本的就会有问题了，8以下的版本到这里就可以结束了。**



事实上并没有启动network服务，而是：

```
Redirecting to /bin/systemctl reatart network.service
Failed to restart network.service: Unit network.service not found
```



**查了很多资料才发现centos 8.x 已经替换了原来的network, 新版的叫：NetworkManager，下面给出解决办法**



- 首先安装NetworkManager

```
yum install NetworkManager*
```



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164807.png)



- 启动NetworkManager

```
service NetworkManager restart
```



- 开启NetworkManager网络服务



```
systemctl status NetworkManager
```



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164812.png)





## 4】验证网络



- 在Windows终端ping我们CentOS的IP：192.168.0.107，可以正常通信。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403164705.png)



- 在CentOS验证一下，也是完全🆗



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403173110.png)



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Linux%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE-CentOS%E7%94%B1NAT%E6%A8%A1%E5%BC%8F%E6%94%B9%E4%B8%BA%E6%A1%A5%E6%8E%A5%E6%A8%A1%E5%BC%8F/QQ%E5%9B%BE%E7%89%8720200403173531.png)



**一番折腾下来，花费了不少时间，尤其是NetworkManager那里，都不想写这篇文章了，但是又想解决这个困难，希望对有需要朋友的有点帮助！**


参考：

[centos7输入systemctl status network.service出现Unit network.service could not be found的解决办法](https://blog.csdn.net/YXWik/article/details/103163492)


[Failed to restart network.service: Unit network.service not found](https://blog.csdn.net/qq_40162735/article/details/101780012)