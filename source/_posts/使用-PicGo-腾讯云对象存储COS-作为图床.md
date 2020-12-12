---
title: 使用 PicGo+腾讯云对象存储COS 作为图床
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-27 21:34:21
password:
summary: 选择PicGo+对象存储COS图床来储存文章图片，优化访问速度也为了更加方便。
tags:
- PicGo
- COS
categories:
- 图床
---

随着博客文章的增加，网站的访问速度也变慢了，尤其是图片使用比较多的文章，在本地还得一张一张添加，更新到<font color=red size=3>CSDN</font>还得重新上传一次，有时候还会出现图片丢失问题。

于是我考虑弄个图床来储存文章图片，优化访问速度也为了更加方便。由于我的域名、服务器在腾讯云，所以就选择<font color=red size=3>PicGo</font>+对象存储<font color=red size=3>COS</font>；看了一下网上关于腾讯云<font color=red size=3>COS</font>作为图床的教程还是挺少的，所以写这篇文章记录一下。

# 一、腾讯云COS配置 #
据了解腾讯云<font color=red size=3>COS</font>以前有<font color=red size=3>50G</font>永久免费额度，2019-01-25之后腾讯云对象存储<font color=red size=3>COS</font>免费额度作了调整，现在是<font color=red size=3>50G</font>免费六个月。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/01.png)

其次，我觉得续费也不是很贵，节约一点还是有的，而且六个月到期不使用了也可以。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/02.png)

现在腾讯云使用需要实名认证，没有实名认证的朋友先去认证吧，也不麻烦。

## 1.创建存储桶 ##

进入【对象存储】→【存储桶列表】→【创建存储桶】

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/03.png)


- 访问权限选择**公有读私有写**，否则图片无法读取，其他的根据自己往下填写就可以。

- 地域建议和你网站地区一样。
## 2.密钥配置 ##

点击【密钥管理】→【云API密钥】→【新建密钥】

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/04.png)

生成的密钥我们后面会用到。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/05.png)

# 二、配置PicGo #

> `PicGo` 是一款开源跨平台的免费图片上传工具以及图床相册管理软件，它能帮你快速地将图片上传到微博、又拍云、阿里云 OSS、腾讯云 `COS`、七牛、`GitHub`、`sm.ms`、`Imgur` 等常见的免费图床网站或云存储服务上，并自动复制图片的链接到剪贴板里，使用上非常高效便捷。

## 1.下载PicGo ##
首先进入[PicGo-Github项目地址](https://github.com/Molunerfinn/PicGo/releases)下载相应版本：


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/06.png)

- `Windows`下载我标记的版本，`Linux`、`mac`都有标明。

下载速度真的是龟速，需要的小伙伴可以在<font color=red size=3>CSDN</font>下载[PicGo-Setup-2.2.2.exe压缩](https://download.csdn.net/download/fugary/12202829),找我拿2.1.2版本也可以。

## 2.配置PicGo ##

打开软件，点击【腾讯云COS】，首先将我们上面创建的<font color=red size=3>API</font>密钥粘贴

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/07.png)

然后来到我们的【储存桶列表】，将存储桶名称、地域填入<font color=red size=3>PicGo</font>，域名为空即可

记得设为默认图床，否则上传不会默认走腾讯云<font color=red size=3>COS</font>。


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/08.png)

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/09.png)
## 3.上传图片 ##

拖拽图片到<font color=red size=3>PicGo</font>，再打开<font color=red size=3>COS</font>就可以看到图片已经上传，使用的时候直接粘贴链接就可以了。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/10.png)

<font color=red size=3>PicGo</font>还有相册功能，可以对已上传的图片进行删除，修改链接等快捷操作，<font color=red size=3>PicGo</font>还可以生成不同格式的链接、支持批量上传、快捷键上传、自定义链接格式、上传前重命名等，以后还可以使用<font color=red size=3>PicGo</font>+<font color=red size=3>GitHub</font>作为图床。

# 使用COS客户端 #
如果不喜欢使用<font color=red size=3>PicGo</font>的话，还可以下载<font color=red size=3>COS</font>客户端，下载相应版本就可以。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/11.png)

然后登录跟之前<font color=red size=3>PicGo</font>差不多，进去页面跟<font color=red size=3>PicGo</font>相差无几。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8-PicGo-%E8%85%BE%E8%AE%AF%E4%BA%91%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8COS-%E4%BD%9C%E4%B8%BA%E5%9B%BE%E5%BA%8A/12.png)

# 使用方法 #

简单说一下，进入对象存储桶，找到你的照片，点击右边【详情】，然后把对象地址复制粘贴到markdown就可以了。

**完**