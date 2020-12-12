---
title: 使用GitHub备份Hexo博客源文件
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-07 15:52:42
password:
summary: Hexo 博客是静态托管的，仓库只有生成的静态网页文件，并没有Hexo的源文件。
tags:
- Hexo
- Github
categories:
- Blog
---


可能有的小伙伴认为备份不就创建一个仓库多简单；或者说我将Hexo博客源文件拷贝到U盘不就可以了吗，可是你写一篇文章或者更新一次配置就要拷贝一次不是很麻烦吗？

备份博客源文件的好处：

- 如果电脑突然罢工，我们的源文件也不会丢失。

- 有时候不方便需要更换电脑写作，我们直接clone仓库就可以了。 

开始我也认为创建一个仓库就可以，可是clone下来的文件却是这样？



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407160040.png)


> 原因： Hexo 博客是静态托管的，仓库只有生成的静态网页文件，并没有Hexo的源文件。




# 备份步骤 #

- 创建一个仓库用来存放备份文件，名字随便，勾选README。

----------

- **复制仓库地址，运行Git将仓库clone到本地。**



```
git clone git@github.com:MUYIio/hexo-themes-matery.git
//git@github.com:MUYIio/hexo-themes-matery.git 改为你自己的
```




![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407184959.png)



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407184949.png)

----------

- **将要备份的文件放到我们刚才clone的文件夹里面。**

  

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407185003.png)

----------

- **在clone的文件夹下运行Git（免得切换cd XXX），依次输入以下命令就可以了。**

```bash
git add .
git commit  -m  "backup"  （注：“backup”里面换成你需要，如“first commit”）
git push -u origin master   （注：此操作目的是把本地仓库push到github上面，如果没有使用密钥此步骤需要你输入帐号和密码）
```


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407184955.png)

----------

- **最后打开我们的仓库就可以看到已经上传了。**





![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/%E4%BD%BF%E7%94%A8GitHub%E5%A4%87%E4%BB%BDHexo%E5%8D%9A%E5%AE%A2%E6%BA%90%E6%96%87%E4%BB%B6/QQ%E5%9B%BE%E7%89%8720200407185007.png)


