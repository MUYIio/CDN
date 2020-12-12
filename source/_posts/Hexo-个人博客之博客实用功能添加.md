---
title: Hexo-个人博客之博客实用功能添加
top: true
cover: false
toc: true
mathjax: true
date: 2020-02-24 21:25:20
password:
summary: 本文以作者blinkfox的matery主题为例，对主题进行了优化，添加了一部分功能。
tags:
- Hexo
- GitHub
- 博客优化
categories:
- Blog
---




本文以作者[blinkfox](https://github.com/blinkfox)的[matery](https://github.com/blinkfox/hexo-theme-matery)主题为例，对主题的部分地方进行优化，添加了一部分功能。

**没有博客？**

[Github + Hexo 搭建个人博客超详细教程](https://www.muyiio.com/2020/02/18/github-hexo-da-jian-ge-ren-bo-ke-chao-xiang-xi-jiao-cheng/#toc-heading-20)

**获取我配置好的主题？**

```javascript
git clone git@github.com:MUYIio/hexo-themes-matery.git
```

**须知：** 不同的<font color=red size=3>Hexo</font>主题的美化方式可能存在一些差异，但也相差无几，把源代码放在合适的位置就可以。

**前提条件：** 进行博客主题美化前需要了解<font color=red size=3>Hexo</font>博客的目录结构，主题的目录结构！请阅读官方文档。了解<font color=red size=3> HTML</font>、<font color=red size=3>CSS</font>、<font color=red size=3>JS</font>，了解 <font color=red size=3>CSS </font>预处理语言 <font color=red size=3>Sass</font>、<font color=red size=3>Less</font>、<font color=red size=3>Stylus</font>,有一定的前端知识最好。

# 1】添加gittalk评论插件 #

<font color=red size=3>matery</font>主题自带<font color=red size=3>gittalk</font>评论插件，我们只需要开启就可以了。

1.打开[GitHub](https://github.com/settings/applications/new)申请，填写信息：

```javascript
Application name //应用名称，随便填
Homepage URL //填自己的博客地址
Application description //应用描述，随便填
Authorization callback URL //填自己的博客地址
```


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/04.png)

2.打开<font color=red size=3>themes/_config.yml</font>下修改<font color=red size=3>gitalk</font>那里：

```javascript
gitalk:
  enable: true
  owner: 你的github用户名
  repo: 你的github用户名.github.io
  oauth:
	clientId: 粘贴刚刚注册完显示的字符串
	clientSecret: 粘贴刚刚注册完显示的字符串
  admin: 你的github用户名
```

添加完成。

------



# 2】添加Valine评论系统

**1.进入[LeanCloud](![image-20200417123325676](C:\Users\残废\AppData\Roaming\Typora\typora-user-images\image-20200417123325676.png))官网注册账户，需要实名认证以及邮箱验证**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/14.png)



**2.创建应用**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/15.png)



**3.进入我们创建的应用，将`AppID`、`AppKey`粘贴到我们的主题配置文件`_config`中**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/16.png)



```bash
valine:
  enable: true
  appId: 
  appKey: 
  notify: true      #评论回复提醒
  verify: false     #验证码
  visitor: false    #他人可见
  avatar: 'wavatar' # Gravatar style : mm/identicon/monsterid/wavatar/retro/hide
  pageSize: 10
  placeholder: '如果你没有GitHub账号，还可以在这里评论啦！' # Comment Box placeholder
```



如果没有上面的配置代码，自己添加就可以。

**4.最后更新就可以了，添加邮件通知、云引擎等等可以自己添加**

------



# 3】添加RSS订阅 #

> 简易信息聚合是“Really Simple Syndication”或“Richsite summary”(网站内容摘要)的中文名字。是站点用来和其他站点之间共享内容的一种简易方式。英文缩写为RSS技术。

> RSS是一种信息聚合的技术，是某一站点和其他站点之间共享内容的一种简易信息发布与传递的方式，使得一个网站可以方便的调用其他提供RSS订阅服务的网站内容，从而形成非常高效的信息聚合，让网站发布的内容在更大的范围内传播。他是一种用于共享新闻和其他WEB内容的数据交换规范，也是使用最广泛的一种扩展性标识语言。


**安装：**

1.在本地<font color=red size=3>hexo</font>目录下右键<font color=red size=3>git bash here</font>，输入以下命令：

```javascript
npm install hexo-generator-feed
```

2.安装完成后，打开<font color=red size=3>hexo</font>目录下配置文件的<font color=red size=3>_config.yml</font>，在末尾添加以下代码：

```javascript
# Extensions
## Plugins: http://hexo.io/plugins/
#RSS订阅
plugin:
- hexo-generator-feed
#Feed Atom
feed:
type: atom
path: atom.xml
limit: 20
```

3.最后打开主题配置文件<font color=red size=3>themes/_config.yml</font>，添加以下代码：

```javascript
rss: /atom.xml
```

现在<font color=red size=3>RSS</font>订阅就添加完成。

# 4】增加建站时间 #

1.在<font color=red size=3>/themes/matery/layout/_partial/footer.ejs</font>最后加上以下代码：

```javascript
<script language=javascript>
    function siteTime() {
        window.setTimeout("siteTime()", 1000);
        var seconds = 1000;
        var minutes = seconds * 60;
        var hours = minutes * 60;
        var days = hours * 24;
        var years = days * 365;
        var today = new Date();
        var todayYear = today.getFullYear();
        var todayMonth = today.getMonth() + 1;
        var todayDate = today.getDate();
        var todayHour = today.getHours();
        var todayMinute = today.getMinutes();
        var todaySecond = today.getSeconds();
        /* Date.UTC() -- 返回date对象距世界标准时间(UTC)1970年1月1日午夜之间的毫秒数(时间戳)
        year - 作为date对象的年份，为4位年份值
        month - 0-11之间的整数，做为date对象的月份
        day - 1-31之间的整数，做为date对象的天数
        hours - 0(午夜24点)-23之间的整数，做为date对象的小时数
        minutes - 0-59之间的整数，做为date对象的分钟数
        seconds - 0-59之间的整数，做为date对象的秒数
        microseconds - 0-999之间的整数，做为date对象的毫秒数 */
        var t1 = Date.UTC(2017, 09, 11, 00, 00, 00); // 北京时间2018-2-13 00:00:00
        var t2 = Date.UTC(todayYear, todayMonth, todayDate, todayHour, todayMinute, todaySecond);
        var diff = t2 - t1;
        var diffYears = Math.floor(diff / years);
        var diffDays = Math.floor((diff / days) - diffYears * 365);
        var diffHours = Math.floor((diff - (diffYears * 365 + diffDays) * days) / hours);
        var diffMinutes = Math.floor((diff - (diffYears * 365 + diffDays) * days - diffHours * hours) / minutes);
        var diffSeconds = Math.floor((diff - (diffYears * 365 + diffDays) * days - diffHours * hours - diffMinutes * minutes) / seconds);
        document.getElementById("sitetime").innerHTML = "本站已运行 " +diffYears+" 年 "+diffDays + " 天 " + diffHours + " 小时 " + diffMinutes + " 分钟 " + diffSeconds + " 秒";
    }
    siteTime();
</script>
```


2.然后在自己想添加的地方（比如网站底部）添加以下代码：

```javascript
<span id="sitetime"></span>
```

# 5】添加404页面 #

1.在<font color=red size=3>/source/</font>目录下新建一个<font color=red size=3>404.md</font>，加上以下代码：

```javascript
---
title: 404
date: 2019-07-19 16:41:10
type: "404"
layout: "404"
description: "页面丢失了 :("
---
```

2.然后在<font color=red size=3>/themes/matery/layout/</font>目录下新建一个<font color=red size=3>404.ejs</font>文件，代码如下：

```javascript
<style type="text/css">
    /* don't remove. */
    .about-cover {
        height: 75vh;
    }
</style>

<div class="bg-cover pd-header about-cover">
    <div class="container">
        <div class="row">
            <div class="col s10 offset-s1 m8 offset-m2 l8 offset-l2">
                <div class="brand">
                    <div class="title center-align">
                        404
                    </div>
                    <div class="description center-align">
                        <%= page.description %>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<script>
  
    $('.bg-cover').css('background-image', 'url(/medias/banner/' + new Date().getDay() + '.jpg)');
</script>
```


添加完成。

# 6】文章图片水印 #

1.在博客根目录下新建一个<font color=red size=3>watermark.py</font>，代码如下：


​    
```javascript
# -*- coding: utf-8 -*-
import sys
import glob
from PIL import Image
from PIL import ImageDraw
from PIL import ImageFont
def watermark(post_name):
    if post_name == 'all':
        post_name = '*'
    dir_name = 'source/_posts/' + post_name + '/*'
    for files in glob.glob(dir_name):
        im = Image.open(files)
        if len(im.getbands()) < 3:
            im = im.convert('RGB')
            print(files)
        font = ImageFont.truetype('STSONG.TTF', max(30, int(im.size[1] / 20)))
        draw = ImageDraw.Draw(im)
        draw.text((im.size[0] / 2, im.size[1] / 2),
                  u'@yourname', fill=(0, 0, 0), font=font)
        im.save(files)
if __name__ == '__main__':
    if len(sys.argv) == 2:
        watermark(sys.argv[1])
    else:
        print('[usage] <input>')
```




写完一篇文章可以运行<font color=red size=3>python3 watermark.py postname</font>添加水印，如果第一次运行要给所有文章添加水印，可以运行<font color=red size=3>python3 watermark.py all</font>。

# 7】添加背景音乐 #

1.首先打开网易云网页版，找到想听的歌曲，然后点击生成外链：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/01.png)

2.选择尺寸，复制代码：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/02.png)

3.然后把代码直接放到文章中就可以了：


![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/03.png)


写完文章上传就可以看到了。



# 8】配置音乐播放器

1.首先，在你的博客 <font color=red size=3>source</font> 目录下的 <font color=red size=3>_data</font> 目录（没有的话就新建一个）中新建 <font color=red size=3>musics.json</font>文件，文件内容如下所示：

```json
[{
	"name": "涩",
	"artist": "纣王老胡",
	"url": "http://xxx.com/music1.mp3",
	"cover": "http://xxx.com/music-cover1.png"
}, {
	"name": "Take me hand",
	"artist": "DAISHI DANCE,Cecile Corbel",
	"url": "/medias/music/music2.mp3",
	"cover": "/medias/music/cover2.png"
}, {
	"name": "Shape of You",
	"artist": "J.Fla",
	"url": "http://xxx.com/music3.mp3",
	"cover": "http://xxx.com/music-cover3.png"
}]
```



> 以上 JSON 中的属性：`name`、`artist`、`url`、`cover` 分别表示音乐的名称、作者、音乐文件地址、音乐封面。



2.然后，在主题的 <font color=red size=3>_config.yml</font> 配置文件中激活配置即可：



```yamly
# 是否在首页显示音乐.

music:
  enable: true
  showTitle: false
  title: 听听音乐
  fixed: false # 是否开启吸底模式
  autoplay: false # 是否自动播放
  theme: '#42b983'
  loop: 'all' # 音频循环播放, 可选值: 'all', 'one', 'none'
  order: 'list' # 音频循环顺序, 可选值: 'list', 'random'
  preload: 'auto' # 预加载，可选值: 'none', 'metadata', 'auto'
  volume: 0.7 # 默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效
  listFolded: false # 列表默认折叠
  listMaxHeight: # 列表最大高度
```



# 9】修改社交链接

1.在主题的 <font color=red size=3>_config.yml</font> 文件中，默认支持 <font color=red size=3>QQ</font>、<font color=red size=3>GitHub</font> 和邮箱的配置，你可以在主题文件的 <font color=red size=3>/layout/_partial/social-link.ejs</font> 文件中，新增、修改你需要的社交链接地址，增加链接可参考如下代码：

```htmlh
<a href="https://github.com/blinkfox" class="tooltipped" target="_blank" data-tooltip="访问我的GitHub" data-position="top" data-delay="50">
    <i class="fa fa-github"></i>
</a>
```



2.其中，社交图标（如：`fa-github`）你可以在 [Font Awesome](https://fontawesome.com/icons) 中搜索找到。以下是常用社交图标的标识，供你参考：

- Facebook: `fa-facebook`

- 微信: `fa-wechat`

- QQ: `fa-qq`

- Twitter: `fa-twitter`
- github：`fa-github`
- Google：`fa-goodle`


官网速度比较慢也可以访问这个网站： [FontAwesome 4.7.0 中完整的675个图标样式CSS参考 ](https://9iphp.com/fa-icons) 

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/05.png)

> 本主题中使用的 `Font Awesome` 版本为 `4.7.0`，使用`font awesome`图标版本也需要对应，不然无法显示。

**如果需要更改<font color=red size=3>font awesome</font>版本，在<font color=red size=3>themes/matery/source/libs/awesome/css</font>文件夹下更换相应版本就可以，5.x版本的图标挺好看的。**


另外，图标使用非常广泛，比如你可以添加在博客页脚等等，具体自己摸索

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/06.png)

# 10】添加博客首页搜索功能

1.安装插件

```bashb
npm install hexo-generator-search --save
```

2.在 Hexo 根目录下的 <font color=red size=3>_config.yml</font> 文件中，新增以下的配置项：

```yamly
search:
  path: search.xml
  field: post
```



# 11】新建友情连接 friends 页

具体的主题配置已经完成。

只需要自己新增<font color=red size=3>friends</font>链接就可以， <font color=red size=3>source</font> / <font color=red size=3>_data</font> /<font color=red size=3>friends.json</font> 文件，文件内容如下所示：

```json
[{
    "avatar": "http://image.luokangyuan.com/1_qq_27922023.jpg",
    "name": "码酱",
    "introduction": "我不是大佬，只是在追寻大佬的脚步",
    "url": "http://luokangyuan.com/",
    "title": "前去学习"
}, {
    "avatar": "http://image.luokangyuan.com/4027734.jpeg",
    "name": "闪烁之狐",
    "introduction": "编程界大佬，技术牛，人还特别好，不懂的都可以请教大佬",
    "url": "https://blinkfox.github.io/",
    "title": "前去学习"
}, {
    "avatar": "http://image.luokangyuan.com/avatar.jpg",
    "name": "ja_rome",
    "introduction": "平凡的脚步也可以走出伟大的行程",
    "url": "ttps://me.csdn.net/jlh912008548",
    "title": "前去学习"
}]


```



> 根据自己需要修改

# 12】添加百度统计 #

> 全球最大的中文网站流量分析平台，帮助企业收集网站访问数据，提供流量趋势、来源分析、转化跟踪、页面热力图、访问流等多种统计分析服务，同时与百度搜索、百度推广、云服务无缝结合，为网站的精细化运营决策提供数据支持，进而有效提高企业的投资回报率。



进入[百度统计首页](https://tongji.baidu.com/web/welcome/login)选择站长版注册登录；点击左上角【管理】，右边【新增网站】填写自己的网站域名，然后获取代码复制下来：

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/07.png)



然后把代码复制到<font color=red size=3>themes/matery/layout/_partial/head.ejs</font>



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/08.png)

上传之后等一会点击【代码安装检查】就可以看到成功了。

------



# 13】添加CNZZ网站统计

**1.进入[友盟](www.cnzz.com)官网注册账户**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/12.png)

**2.添加站点**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/13.png)

**3.将代码复制粘贴到`footer.ejs`（任选一种样式就可以）**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/10.png)

**4.效果预览**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/11.png)



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E4%B9%8B%E5%8D%9A%E5%AE%A2%E5%AE%9E%E7%94%A8%E5%8A%9F%E8%83%BD%E6%B7%BB%E5%8A%A0/09.png)



**持续更新中...**

