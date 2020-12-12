---
title: Hexo 双线部署到 Coding Pages 和 GitHub Pages 提升访问速度
top: false
cover: false
toc: true
mathjax: true
date: 2020-02-20 23:15:24
password:
summary: 为了摆脱GitHub的龟速暴击，我们选择把博客托管到Coding来提升访问速度。
tags:
- Hexo
- Coding
- HTTPS
categories:
- Blog
---

<font color=magenta size=4>**在操作过程中遇到问题欢迎来骚扰我哈！<font color=red size=4> V：godxiaolong，QQ:1571504536</font>**</font>

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/001.png)

相信不少朋友用<font color=red size=3>Hexo+Github</font>搭建博客后，会发现网站的访问速度简直是龟速。为了摆脱<font color=red size=3>GitHub</font>的龟速暴击，我们选择把博客托管到<font color=red size=3>Coding</font>来提升访问速度。

至于什么是<font color=red size=3>Coding</font>：
> Coding WebIDE 是 Coding 自主研发的在线集成开发环境 (IDE)。用户可以通过 WebIDE 创建项目的工作空间, 进行在线开发, 调试等操作。同时 WebIDE 集成了 Git 代码版本控制, 用户可以选择 Coding、GitHub、BitBucket、Git@OSC 等任意的代码仓库。 WebIDE 还提供了分享开发环境的功能, 用户可以保存当前的开发环境, 分享给团队的其他成员。大家可以理解为中国版的github，如果把代码既托管到coding上，又托管到github上，让大陆的用户访问的是由coding托管的网站，歪果仁访问的是由github托管的网站，以此来提升我们网站的访问速度。

部署到<font color=red size=3> Coding Pages </font>的好处：国内访问速度更快，可以提交百度收录（<font color=red size=3>GitHub </font>禁止了百度的爬取）

**部署过程中我所遇到的两个问题：**

- 使用密钥连接<font color=red size=3>Coding</font>时出现权限不足的情况；（**已解决**）
- 无法无法实现全站 <font color=red size=3>HTTPS</font>。（**已解决**）

 这两个问题我会在文中给出解决办法。

进行下面操作的前提是你已经将自己的博客推送到<font color=red size=3>GitHub</font>（拥有自己的博客），如果没有，可以参考我之前的文章[《Github + Hexo 博客搭建超详细教程》](https://muyiio.com/2020/02/18/github-hexo-bo-ke-da-jian-chao-xiang-xi-jiao-cheng/ "Github + Hexo 博客搭建超详细教程")

## 文章目录 ##
- 1.创建项目
- 2.配置 <font color=red size=3>_config.yml</font>
- 3.将代码推送到<font color=red size=3>Coding</font>
- 4.开启<font color=red size=3> Coding Pages</font>
- 5.绑定域名并开启<font color=red size=3> Https</font>

-----
# 1.创建项目 #
[点击此处](https://dev.tencent.com/production "Coding")进入<font color=red size=3>Coding</font>个人版官网注册账号，由于 <font color=red size=3>Coding</font> 已经被腾讯收购了，所以登录就会来到[腾讯云](https://cloud.tencent.com/?fromSource=gwzcw.2212127.2212127.2212127&utm_medium=cpd&utm_id=gwzcw.2212127.2212127.2212127)开发者平台：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/01.png)

找到创建项目：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/02.png)

项目名称建议和你的用户名一致，到时候可以直接通过 <font color=red size=3>user_name.coding.me </font>访问你的博客，如果项目名与用户名不一致，则需要通过<font color=red size=3> user_name.coding.me/project_name </font>才能访问，项目描述随便写：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/03.png)

# 2.配置 _config.yml #
进入我们的项目，在右上角选择连接方式，这里我以<font color=red size=3>HTTPS</font>连接为例（SSH就复制**ssh链接**），将链接复制下来：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/04.png)

然后打开你本地博客根目录的<font color=red size=3> _config.yml </font>文件，找到<font color=red size=3> deploy </font>关键字，添加 我们刚才复制的<font color=red size=3> coding </font>地址：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/05.png)

**注意：**

- 1.如果要<font color=red size=3>同时</font>推送到<font color=red size=3>GitHub</font>和<font color=red size=3>Coding</font>，<font color=red size=3>type</font>前面加<font color=red size=3> -</font>。
- 2.每一行<font color=red size=3>冒号后面的空格</font>不要忘记。


**SSH连接**

1.相信小伙伴们已经把博客部署在<font color=red size=3>GitHub</font>。这里操作是一样的，鼠标移动到【头像】→【个人设置】→【SSH公钥】，把我们的密钥复制粘贴到coding。

2.配置本地文件

贴上我的


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/QQ%E5%9B%BE%E7%89%8720200329214201.png)

3.连接coding

    ssh -T git@e.coding.net

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/QQ%E5%9B%BE%E7%89%8720200330102625.png)

**我之前不选择SSH连接Coding的原因**：

- 1.我的<font color=red size=3>SSH</font>连接<font color=red size=3>GitHub</font>没有问题，但是连接<font color=red size=3>Coding</font>就显示没有权限。


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/06.png)

> 原因是：以前的连接代码是ssh -T git@git.coding.net


# 3.将代码推送到Coding #
现在我们在博客根目录下右键单击<font color=red size=3>Git Bash Here</font>，输入下面三个命令：

    hexo clean 
    hexo g
    hexo d

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/07.png)

使用<font color=red size=3>HTTPS</font>的缺点就是在推送时会要求我们输入<font color=red size=3>Coding</font>的用户名和密码，如果第一次输入错误了，可以参考这篇资料：

[git本地第一次推送密码填写错误处理方式](https://blog.csdn.net/qq_38948398/article/details/89953365?utm_source=app "git本地第一次推送密码填写错误处理方式") (By 颜墨白)

# 4.开启 Coding Pages #
进入你的项目，在构建与部署一栏选择静态网站，这里需要实名认证：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/08.png)

选择我们的代码库：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/09.png)

这个时候就可以看到我们的网站地址啦：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/10.png)

# 5.绑定域名并开启 Https #
在静态网站一栏右上角点击设置，下滑到底绑定我们的域名（注意：<font color=red size=3>www.xxx.com </font>开头）：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/11.png)

然后打开我们的域名解析，我在之前的文章中详细介绍了关于域名解析[《Github + Hexo 博客搭建超详细教程》](https://muyiio.com/2020/02/18/github-hexo-bo-ke-da-jian-chao-xiang-xi-jiao-cheng/ "Github + Hexo 博客搭建超详细教程")，两种方法：

- 1.在域名<font color=red size=3> DNS </font>设置中添加一条<font color=red size=3> CNAME </font>记录指向 <font color=red size=3>xxxx.coding.me</font>，解析路线选择默认。
- 2.在域名<font color=red size=3> DNS </font>设置中添加一条<font color=red size=3>A</font>记录，记录指向<font color=red size=3> xxxx.coding.me</font>的<font color=red size=3>ip</font>，解析路线选择默认。（<font color=red size=3>ip地址获取：WIN+R输入cmd进入终端，输入：ping xxxx.coding.me 即可。</font>）

将 <font color=red size=3>GitHub</font> 的解析路线改为 境外，这样境外访问就会走<font color=red size=3> GitHub</font>，境内就会走<font color=red size=3> Coding</font>，也有人说阿里云是智能解析，自动分配路线，如果解析路线都是默认，境外访问同样会智能选择走<font color=red size=3> GitHub</font>，境内走 <font color=red size=3>Coding</font>。

我的解析：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/12.png)

**<font color=red size=3>SSL</font>证书申请失败解决方法：**

- 先去域名 <font color=red size=3>DNS</font> 把 G<font color=red size=3>itHub</font> 的解析暂停掉，然后再重新申请 <font color=red size=3>SSL</font> 证书，大约十秒左右就能申请成功，然后开启强制 <font color=red size=3>HTTPS 访问</font>


**开启<font color=red size=3>HTTPS</font>,如图，勾选即可：**
![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8F%8C%E7%BA%BF%E9%83%A8%E7%BD%B2%E5%88%B0-Coding-Pages-%E5%92%8C-GitHub-Pages-%E6%8F%90%E5%8D%87%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6/13.png)


文章中难免有错误的地方，有大佬发现了欢迎给我指正！有的地方解释不够详细，可以百度一下看看细节，文章中的引用以及参考资料涉及侵权请联系我删除！
