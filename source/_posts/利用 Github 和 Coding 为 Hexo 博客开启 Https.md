---
title: 利用 Github 和 Coding 为 Hexo 博客开启 Https
top: false
cover: false
toc: true
mathjax: true
date: 2020-02-24 21:33:26
password:
summary: 本文记录使用Github和Coding官方支持为我们的Hexo博客开启Https。
tags:
- Https
- Hexo
categories:
- Blog
---

本文记录使用<font color=red size=3>Github</font>和<font color=red size=3>Coding</font>官方支持为我们的<font color=red size=3>Hexo</font>博客开启<font color=red size=3>Https</font>

> HTTP是一个简单的请求-响应协议，它通常运行在TCP之上。它指定了客户端可能发送给服务器什么样的消息以及得到什么样的响应。请求和响应消息的头以ASCII码形式给出；而消息内容则具有一个类似MIME的格式。


> HTTPS （全称：Hyper Text Transfer Protocol over SecureSocket Layer），是以安全为目标的 HTTP 通道，在HTTP的基础上通过传输加密和身份认证保证了传输过程的安全性 [1]  。HTTPS 在HTTP 的基础下加入SSL 层，HTTPS 的安全基础是 SSL，因此加密的详细内容就需要 SSL。 HTTPS 存在不同于 HTTP 的默认端口及一个加密/身份验证层（在 HTTP与 TCP 之间）。


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E5%88%A9%E7%94%A8%20Github%20%E5%92%8C%20Coding%20%E4%B8%BA%20Hexo%20%E5%8D%9A%E5%AE%A2%E5%BC%80%E5%90%AF%20Https/04.png)

# 使用GitHub开启Https #
目前利用<font color=red size=3>GitHub Pages</font>的网站都可以开启<font color=red size=3>Https</font>，不论是自定义域名还是官方的二级域名。

首先来到我们的域名解析：

如果你域名的记录类型是 <font color=red size=3>CNAME</font> 方式，那么就不需要做任何更改；

域名的记录类型是<font color=red size=3> A </font>方式，那么就需要把记录值指向以下<font color=red size=3>IP</font>地址：

- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

我的解析是在腾讯云，<font color=red size=3>A</font>记录只能添加四个，<font color=red size=3>GitHub</font>和<font color=red size=3>Coding</font>就只能分配2个，所以上面的<font color=red size=3>IP</font>我只解析了一个，不过阿里云好像可以解析多个，自己看着办。

可以参考一下我的：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E5%88%A9%E7%94%A8%20Github%20%E5%92%8C%20Coding%20%E4%B8%BA%20Hexo%20%E5%8D%9A%E5%AE%A2%E5%BC%80%E5%90%AF%20Https/01.png)

域名解析好了之后打开<font color=red size=3>GitHub</font>仓库，点击【<font color=red size=3>Settings</font>】：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E5%88%A9%E7%94%A8%20Github%20%E5%92%8C%20Coding%20%E4%B8%BA%20Hexo%20%E5%8D%9A%E5%AE%A2%E5%BC%80%E5%90%AF%20Https/02.png)

勾选【<font color=red size=3>Enforce HTTPS</font>】，注意：如果此时你不能勾选，请删除【<font color=red size=3>Custom domain</font>】里面你的域名并点击【<font color=red size=3>Save</font>】保存，刷新网页后就可以勾选了

# 使用Coding开启Https #
**如果你的博客还没有托管到<font color=red size=3>Coding</font>，可以参照我另外一篇文章：**
[Hexo 双线部署到 Coding Pages 和 GitHub Pages 提升访问速度](https://muyiio.com/2020/02/20/hexo-shuang-xian-bu-shu-dao-coding-pages-he-github-pages-ti-sheng-fang-wen-su-du-bing-shi-xian-quan-zhan-https/ "赵晓龙的博客")

进入我们的<font color=red size=3>Coding</font>项目，点击【<font color=red size=3>构建与部署</font>】-【<font color=red size=3>静态网站</font>】，再点击右上角的设置，下拉到底部勾选【<font color=red size=3>强制 HTTPS</font>】。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E5%88%A9%E7%94%A8%20Github%20%E5%92%8C%20Coding%20%E4%B8%BA%20Hexo%20%E5%8D%9A%E5%AE%A2%E5%BC%80%E5%90%AF%20Https/03.png)

**这里说明一下：**

<font color=red size=3>Coding</font>绑定域名后<font color=red size=3>SSL</font>证书申请失败，去域名解析把<font color=red size=3>GitHub</font>解析暂停就可以申请成功了。

参照：[hexo双线部署coding+github pages，实现https并开启又拍云CDN全站加速](https://blog.csdn.net/qq_41793001/article/details/102995817?utm_source=app)

