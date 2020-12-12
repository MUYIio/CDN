---
title: Hexo博客提交百度收录SEO
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-07 23:27:53
password:
summary: 我们需要手动给搜索引擎提交收录，别人在搜索到关键词时就看到我们的文章
tags:
- Hexo
- SEO
categories:
- Blog
---



## 1】前言

博客也搭建了几个月了，在百度/Google都没有提交收录，于是记录一下提交收录的过程。

对于Hexo博客而言，我们需要手动给搜索引擎提交收录，这样别人在搜索到文章关键词时才能够看到我们的文章，才能增加曝光率。



Github禁止了百度爬取，如果只是部署到了GitHub，是无法进行收录的。可以考虑同时部署在Coding，然后进行百度收录。参考教程：



[Hexo 双线部署到 Coding Pages 和 GitHub Pages 提升访问速度 ](https://www.muyiio.com/2020/02/20/hexo-shuang-xian-bu-shu-dao-coding-pages-he-github-pages-ti-sheng-fang-wen-su-du/)



## 2】查看网站是否收录

- 输入`site:域名`查看我们的网站是否收录

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200408213911.png)



由于我之前提交过，所以有记录，正常情况下是查询不到信息的。



## 3】百度搜索资源平台添加网站

-  **首先进入[百度资源搜索平台](https://ziyuan.baidu.com)注册登录（使用百度联盟账号也可以）**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200408215041.png)



- **点击【用户中心】→【站点管理】添加网站**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200408214859.png)



 **协议开头建议Https://**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200407233807.png)



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200407233800.png)



- **验证站点**（推荐两个方法）



1.HTML标签验证



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200407233813.png)



放到`head.ejs`，`<head> `与 `</head> `标签之间



2.CNAME验证



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200409003519.png)

在DNS添加这条解析就可以了，生效可能得等一会。



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200409003525.png)



## 4】提交链接

- **主动推送**

1.安装插件：



```bash
npm install hexo-baidu-url-submit --save
```



2.在根目录 `_config.yml` 文件里加入以下代码：



```bash
baidu_url_submit:
  count: 100                 # 提交最新的多少个链接
  host: www.muyiio.com       # 在百度站长平台中添加的域名
  token:                     # 秘钥
  path: baidu_urls.txt
```



`token`可以在推送接口下面看到：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200409003532.png)



3.在根目录的 `_config.yml` 下找到以下配置：



```bash
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://www.muyiio.com
root: /
permalink: :year/:month/:day/:title/
```



`url:`后面填写在百度添加的域名



4.在`_config.yml` 加入新的` deployer`

- ```bash
  deploy:
  - type: git
    repository:
      github: git@github.com:MUYIio/MUYIio.github.io.git
      coding: git@e.coding.net:godxiaolon/godxiaolon.git
      repo: root@118.25.27.52:/home/git/blog.git
    branch: master
  - type: baidu_url_submitter        #新加的主动推送
  ```

  

5.最后三连上传就可以了,这样显示就是成功

```bash
{"remain":2985,"success":15}           #表示成功15条
INFO  Deploy done: baidu_url_submitter

```



- **自动推送**

1.复制代码

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo%E5%8D%9A%E5%AE%A2%E6%8F%90%E4%BA%A4%E7%99%BE%E5%BA%A6%E6%94%B6%E5%BD%95SEO/QQ%E5%9B%BE%E7%89%8720200409003536.png)



```javascript
<script>
(function(){
    var bp = document.createElement('script');
    var curProtocol = window.location.protocol.split(':')[0];
    if (curProtocol === 'https') {
        bp.src = 'https://zz.bdstatic.com/linksubmit/push.js';
    }
    else {
        bp.src = 'http://push.zhanzhang.baidu.com/push.js';
    }
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
})();
</script>
```



2.放到`\themes\material-x\layout\_partial\head.ejs`的`<head> `与 `</head> `标签之间。



3.如果主题集成了这个功能，比如 next 主题，在 `themes\next\layout_scripts\` 下有个 `baidu_push.swig` 写入下面代码：





```javascript
{% if theme.baidu_push %}
<script>
(function(){
    var bp = document.createElement('script');
    var curProtocol = window.location.protocol.split(':')[0];
    if (curProtocol === 'https') {
        bp.src = 'https://zz.bdstatic.com/linksubmit/push.js';
    }
    else {
        bp.src = 'http://push.zhanzhang.baidu.com/push.js';
    }
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
})();
</script>
```



然后在文件主题配置文件`_config.yml` 中设置 即可。



```bash
baidu_push: true 
```







## 5】总结

- 我只使用了上面两种方法推送，更多的可以自己尝试。
- 收录大概需要半个多月，耐心等待。