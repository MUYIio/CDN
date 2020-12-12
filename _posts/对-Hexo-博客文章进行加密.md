---
title: 对 Hexo 博客文章进行加密
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-12 10:20:37
password:
summary: 有时候我们可能需要写一些私密的博客，通过密码验证的方式让人不能随意浏览。

tags:
- Hexo
categories:
- Blog
---

# 写在前面 #

- 有时候我们可能需要写一些私密的博客，通过密码验证的方式让人不能随意浏览。

- 这在wordpress，emlog或其他博客系统中都很容易实现，然而hexo除外。:(

- 为了解决这个问题，我们需要安装“ hexo-blog-encrypt”扩展。


# 特性 #

- 一旦你输入了正确的密码，它就会被存储在本地浏览器的localStorage中。按个按钮，密码将会被清空。若博客中又脚本，它将被正确地执行。

- 支持按标签加密。

- 所有的核心功能都是由原生的API所提供的。在Node.js中，我们使用Crypto。在浏览器中，我们使用Web Crypto API。

- PBKDF2，SHA256被用作复制密钥，AES256-CBC被用作加解密，我们还使用HMAC来验证密文的来源，并确保其纠正。

- 广泛地使用Promise来进行异步操作，从而确保线程不被杜塞。

- 过时的浏览器将无法正常显示，因此，请升级您的浏览器。


# 安装 #

```javascriptj
npm install --save hexo-blog-encrypt
```

# 快速使用 #

- **将“ <font color=red size=3>password</font>”添加到您的文章信息头就像这样**：
       
  
    ```javascriptj
    title: Hello World
    date: 2020-03-13 21:12:21
    password: muyiio
    ---
    ```





# 按标签加密 #

- **修改文章信息头如下：**



```java
title: Hello World
tags:
- 加密文章tag
date: 2020-03-13 21:12:21
password: muyiio
abstract: 这里有东西被加密了，需要输入密码查看哦。
message: 您好，这里需要密码。
wrong_pass_message: 抱歉，这个密码看着不太对，请再试试。
wrong_hash_message: 抱歉，这个文章不能被纠正，不过您还是能看看解密后的内容。
---
```






- **对博客根目录<font color=red size=3>_config</font>添加如下字段：**



```javascriptj
# 安全
encrypt: # hexo-blog-encrypt
  abstract: 这里有东西被加密了，需要输入密码查看哦。
  message: 您好, 这里需要密码.
  tags:
  - {name: tagName, password: 密码A}
  - {name: tagName, password: 密码B}
  template: <div id="hexo-blog-encrypt" data-wpm="{{hbeWrongPassMessage}}" data-whm="{{hbeWrongHashMessage}}"><div class="hbe-input-container"><input type="password" id="hbePass" placeholder="{{hbeMessage}}" /><label>{{hbeMessage}}</label><div class="bottom-line"></div></div><script id="hbeData" type="hbeData" data-hmacdigest="{{hbeHmacDigest}}">{{hbeEncryptedData}}</script></div>
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
```






# 对 TOC 文章进行加密 #

如果您有一篇文章使用了<font color=red size=3>TOC</font>，您需要修改模板的部分代码。这里以<font color=red size=3>matery</font>主题作为示例：

- **在<font color=red size=3>hexo/themes/matery/layout/_partial/article.ejs</font>找到<font color=red size=3>article.ejs</font>。**

- **然后找到<font color=red size=3><％post.content％></font>这段代码，通常在<font color=red size=3>30</font>行左右。**

- **使用如下的代码来替代它：**
  
    	

```javascriptj
<% if(post.toc == true){ %>
  <div id="toc-div" class="toc-article" <% if (post.encrypt == true) { %>style="display:none" <% } %>>
    <strong class="toc-title">Index</strong>
      <% if (post.encrypt == true) { %>
        <%- toc(post.origin, {list_number: true}) %>
      <% } else { %>
        <%- toc(post.content, {list_number: true}) %>
      <% } %>
  </div>
<% } %>
<%- post.content %>
```



# 声明 #

本文转载自作者[MikeCoder](https://github.com/MikeCoder/hexo-blog-encrypt)的<font color=red size=3>hexo-blog-encrypt</font>项目，对有些地方略有修改。



项目地址：[https://github.com/MikeCoder/hexo-blog-encrypt](https://github.com/MikeCoder/hexo-blog-encrypt)



发现这个还是挺好玩的~