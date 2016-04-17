---
layout: post
title: 使用Jekyll快速搭建博客网站
description: 本文主要介绍如何使用Jekyll快速搭建博客网站，并在本地环境下在调试完成后上线，以及如何绑定自己的域名...
---

## 本地环境的搭建

**＃jekyll的安装**

新建并cd到项目路径，需要用到gem，我用的MacOS自带的。

    $ gem install jekyll
    
这里安装到时候报了错：“Could not find a valid gem in any repository”。

类似的错误应该是因为gem默认的sources是https://rubygems.org/

解决方法如下（这里我顺便把原来的source给删了）：
  
    $ gem sources --add http://rubygems.org/

**＃新建模板**

终端键入：

    $ jekyll new blog

可以看到目录下多了blog目录，里面就是标准的jekyll目录结构了，你要发布的博客页在_post文件夹下，格式是markdown。
每个md文件都带有头部信息，layout用来concat静态文件。

    ---
    layout: post
    title: What's Jekyll-test?
    description: description of your article
    ---
    
每次都要输这些，是挺烦人的。

可以在sublime中自定义个snippet：tool > new snippet

    <snippet>
	<content>
	  <![CDATA[
        ---
        layout: post
        title: ${1:title}
        description: ${2:...}
        ---

        ${3}
      ]]>
    </content>
	<tabTrigger>headinfo</tabTrigger>
	<scope>text.html.markdown</scope>
    </snippet>

保存在User目录下，后缀名**.sublime-snippet**，这样敲headinfo，用tab键补齐，就可以敲出代码块了。

**更多关于目录结构的信息，可以参考[中文官网](http://jekyll.bootcss.com/docs/structure/)上的说明，这里不赘述了。**

接着，构建项目
    
    $ cd blog
    $ jekyll build --watch

构建完成的文件会放在_site文件夹下。

启动jekyll自带的server：

    $ jekyll serve 
    
打开localhost:4000就预览生成后的项目了。

**＃Theme的使用**

jekyll有很多很棒的主题，在主题的基础上再去定制，会省心很多，可以去github上去找找。

这里要注意的是一些主题需要额外安装gem包，而其中有一些包最新的jekyll 3.0已经不再支持，像是代码高亮的pgyments.rb等。

了解更多关于dependencies的情况，点[这里](https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0)。

## 上传到Github

本地测试完成后，就可以推送到Gitpages上部署了,也就是上线。

如果你还不了解如何用Github pages建立及部署页面，[点传送门](https://pages.github.com) 简单几步轻松搞定。

将blog中的文件拷入到你clone到本地的username.gitgithub.io目录中，然后push，github会自动帮你build。要注意的是，如果生成失败，会有一封邮件发送到你的邮箱，并注明错误的原因。改完再推送一次就可以了。

## 域名的绑定

**＃如何绑定自己的域名**

＊在项目根目录下新建CNAME文件，添加你的域名，如我的darkflow.cc，然后push。

＊然后到域名服务商上添加域名解析，需要添加2条记录，类型为CNAME。主机纪录分别为**@**和**www**，记录值为 **username.github.io.**


![域名解析截图]({{ site.baseurl }}public/post_imgs/1.png)

＊过个几分钟就能看到域名映射成功了。
