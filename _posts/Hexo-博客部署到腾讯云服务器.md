---


title: Hexo 博客部署到腾讯云服务器
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-28 20:47:51
password:
summary: 相信大家把博客部署到服务器都是为了加快访问速度，这里就不啰嗦了。
tags:
- Hexo
categories:
- 服务器
---





>  相信大家把博客部署到服务器都是为了加快访问速度，这里就不啰嗦了。



**这篇教程没有使用宝塔Linux面板部署，浏览器访问会显示不安全，如果Hexo博客只部署到服务器，不部署到GitHub或者coding，那么请参照我的另一篇文章，使用宝塔面板更为方便，主要是为了部署SSL。**



**[Hexo博客部署到腾讯云服务器(使用宝塔面板)](https://www.muyiio.com/2020/04/10/shi-yong-bao-ta-mian-ban-yi-jian-bu-shu-hexo-bo-ke/)**



我的服务器

- 系统 `CentOS 7.5 64bit`

- 配置 `标准型S2/1核/2GB/1Mbps`

服务器需要的环境

- 环境：`git`，`Nginx`
- 使用`git` 自动化部署发布

打开腾讯云，进入【云服务器】→【登录】

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/02.png)



>  初始密码在右上角消息里面有



# 1】Git安装及配置



### 一、安装依赖库和编译工具

- 安装依赖库：

  ```c++c
  yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel 
  ```



然后会出现：

```
Is this ok [y/d/N]:
```

输入`y`继续安装，后面也一样。



- 安装编译工具：

  ```
  yum install gcc perl-ExtUtils-MakeMaker package 
  ```



### 二、下载 git并解压编译安装



- 查看服务器已有的git版本

```
git --version
```



然后会看到：

```
git version 1.8.3.1
```



> 但是官网版本已经更新了，因为yum仓库的Git版本更新的时间会存在延时，我们这里采用源码包安装方式安装。



- 将陈旧版本的git删除

```
yum remove git
```



- 选择一个目录来存放下载下来的 git 安装包。这里选择了`/usr/local/src` 目录

  ```
  cd /usr/local/src  
  ```

  

- 下载最新版git到`/usr/local/src`，可以在官网找到版本，目前最新版本是2.26.0。

```
wget http://ftp.ntu.edu.tw/software/scm/git/git-2.26.0.tar.gz
```



- 解压到当前目录

```
tar -zvxf git-2.26.0.tar.gz
```



- 进入 `git-2.26.0.tar.gz` 目录下

```
cd git-2.26.0
```



- 执行编译

```
make prefix=/usr/local/git all
```



- 安装 git 到 /usr/local/git 目录下

```
make prefix=/usr/local/git install
```



### 三、配置 git 环境变量

- 打开环境变量配置文件

```
vim /etc/profile
```

按i进入编辑模式，按向下键到底部，添加下面两行命令：

```
PATH=$PATH:/usr/local/git/bin   # git 的目录
export PATH
```

**按`esc`退出，按`:wq`保存编辑。(注意是先`:`再是`wq`)**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004810.png)



- 使 git 环境变量生效

```
 source /etc/profile
```



- 验证安装完成，查看 git 的版本号

```
git --version
```

这时候我们的git版本已经变成了：

```
git version 2.26.0
```



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004827.png)



###  四、创建 git 用户

- 创建git用户

```
adduser git
```



- 获取权限

```
chmod 740 /etc/sudoers
vim /etc/sudoers
```



按 `i` 键进入文件的编辑模式，按向下键找到如下字段

```
root    ALL=(ALL)       ALL
```

在其后面增加一句：

```
git     ALL=(ALL)       ALL
```

**按 `Esc` 键退出编辑模式，输入`:wq` 保存退出。（先输入`:`，然后输入`wq`回车）**



- 退回权限

```
chmod 400 /etc/sudoers
```



### 五、配置密钥

- 创建密钥

来到这里的小伙伴应该都已经有了自己的hexo博客，那么肯定已经创建过自己的密钥，一般存放在`c/用户/.ssh`下。

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004830.png)

如果没有自己的密钥，可以移步我之前的教程，里面有密钥创建步骤

[Github + Hexo 搭建个人博客超详细教程](https://www.muyiio.com/2020/02/18/1/)



- 将密钥保存在服务器(之前有密钥的直接复制就可以)

将`id_rsa.pub`里面的密钥复制,在服务器运行下面命令，创建.ssh文件夹

```
su git
mkdir ~/.ssh
```



创建`.ssh/authorized_keys`文件，打开`authorized_keys`文件并将刚才在本地机器复制的内容拷贝其中并保存

```
vim ~/.ssh/authorized_keys
```

**按`i`进入编辑模式粘贴完按 `Esc` 键退出编辑模式，输入`:wq` 保存退出。（先输入`:`，然后输入`wq`回车）**



- 修改权限

```
chmod 755 ~
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```



- 测试本地连接服务器

  在本地电脑git bash here

```
//yourIp为远程服务器的ip地址
ssh -v git@yourIp     //yourIp为你的服务器ip
```



如图则证明本地机器与远程机器已经接通

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004834.png)



### 六、创建git仓库

- 切换到root用户，创建一个目录用于存储网站的根目录

```
su root
```



- 创建网站的根目录

```
mkdir /home/hexo
```



- 给予权限

```
chown gitgit -R //hexo
```



# 2】安装Nginx

> *Nginx* (engine x) 是一个高性能的[HTTP](https://baike.baidu.com/item/HTTP)和[反向代理](https://baike.baidu.com/item/反向代理/7793488)web服务器，同时也提供了IMAP/POP3/SMTP[服务](https://baike.baidu.com/item/服务/100571)



### 一、安装配置Nginx

- 安装Nginx

```
yum install -y nginx
```



- 配置Nginx

```
nginx -t
```



使用vim打开nginx.conf文件

```
vim /etc/nginx/nginx.conf
```



**按`i`进入编辑模式粘贴完按 `Esc` 键退出编辑模式，输入`:wq` 保存退出。（先输入`:`，然后输入`wq`回车）**



```j
server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  www.muyiio.com;   //你的博客域名
        root         /home/hexo;       //git仓库目录
    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }
j
    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }
}
```





![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004838.png)



- 启动Nginx

```
systemctl start nginx.service
```



- 重启Nginx

```
systemctl restart nginx.service
```



### 二、自动化部署

- 获取root权限

```
su root
```



- 建立git仓库

```
cd /home/git
git init --bare blog.git
```



- 修改blog.git权限

```
chown git:git -R blog.git
```





- 在 `/home/hexo/blog.git` 下，有一个自动生成的 `hooks` 文件夹，我们创建一个新的 `git` 钩子 `post-receive`，用于自动部署。

```
vim blog.git/hooks/post-receive
```



- **按 `i` 键进入文件的编辑模式**，在该文件中添加两行代码（将下边的代码粘贴进去)，指定 Git 的工作树（源代码）和 Git 目录

```
 #!/bin/bash 
 git --work-tree=/home/hexo --git-dir=/home/git/blog.git checkout -f 
```

**按 `Esc` 键退出编辑模式，输入`:wq` 保存退出。（先输入`：`，然后输入`wq`回车）**



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004843.png)



- 修改文件权限，使得其可执行。

```
chmod +x /home/git/blog.git/hooks/post-receive
```





# 3】配置本地Hexo

- 博客根目录_config下增加

```
deploy:
    type: git
    repo: root@***(服务器ip,内网外网都行):/home/git/blog.git    #仓库地址
    branch: master    #分支
```



- 部署

```
hexo clean
hexo g
hexo d
```



- 输入`hexo d`的时候，会要求你输入自己的服务器密码

```
Branch 'master' set up to track remote branch 'master' from 'https://e.coding.net/godxiaolon/godxiaolon.git'.
On branch master
nothing to commit, working tree clean
root@119.25.56.82's password:
Enumerating objects: 182, done.
Counting objects: 100% (182/182), done.
Delta compression using up to 12 threads
Compressing objects: 100% (61/61), done.
Writing objects: 100% (95/95), 73.08 KiB | 3.18 MiB/s, done.
Total 95 (delta 45), reused 0 (delta 0)
remote: hooks/post-receive: line 1: t: command not found
To 118.25.27.52:/home/git/hexoBlog.git
   8df3691..7d63b39  HEAD -> master
Branch 'master' set up to track remote branch 'master' from 'root@118.25.27.52:/home/git/hexoBlog.git'.
INFO  Deploy done: git
```

>  输入密码不会有显示，输完回车就可以



- **如果出现`bash: git-receive-pack: command not found`,则运行：**

```
sudo ln -s /usr/local/git/bin/git-receive-pack  /usr/bin/git-receive-pack
```



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/_4%7BPJVH2DYU8PVWJT%60A%7BY_Q.png)



- 访问服务器ip，看看有没有成功

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/Hexo-%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0%E8%85%BE%E8%AE%AF%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8/QQ%E5%9B%BE%E7%89%8720200402004847.png)



最后，发现其实挺简单的，快去访问你的服务器`ip`看看有没有部署成功吧