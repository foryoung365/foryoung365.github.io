---

layout: post
title: "用Jekyll在GitHub上搭建个人网站"
description: "用Jekyll在GitHub上搭建个人网站"
category: Tutorial
tags: [Web]
---
{% include JB/setup %}

整理一下建站过程，方便自己，也让后人少走点弯路。以下是基于windows的建站步骤。

在GitHub上建立个人网站的Git仓库
-------------------------------

------------------------------------------------------------------------

1.  到[GitHub](https://github.com/)上申请一个账号，假设用户名为username。
2.  新建一个名字为username.github.io的Git仓库，为什么要这么命名的原因看[这里](https://help.github.com/articles/user-organization-and-project-pages/)。

安装Git和Git的图形界面程序
--------------------------

------------------------------------------------------------------------

个人推荐[SourceTree](http://sourcetreeapp.com/)，内置git，简单易用，同时支持Windows和Mac OS，最重要的还是免费的，我实在是想不出一个不用它的理由。
当然你也可以考虑自己安装[git for windows](http://msysgit.github.io/)。

安装Ruby和jekyll
----------------

------------------------------------------------------------------------

# 在windows下自己安装ruby是个很遭罪的过程，所以我们选择集成安装包[RubyInstaller](http://rubyinstaller.org/)，下载完找个地方解压，这里假设是**D:Ruby**。

# 别忘了把DevKit一起下载下来，要根据你的机器选择32位或者64位版本。解压到**D:DevKit**;

# 打开Ruby命令行执行以下命令：

    D:
    cd D:DevKit
    ruby dk.rb init

# 这时候在DevKit目录下会生成一个**config.yml**文件，打开文件看下，正常情况下应该能够自动找到Ruby的安装路径。如果没有的话，自行添加两行：

     - D:RubyDevKit
     - D:RubyDevKit

# 注意上面两行**-**前后的空格都必须有。接着运行：

    ruby dk.rb install

# 接着我们可以开始安装jekyll了。

    gem install jekyll

# 如果出现无法连接的问题，那就是伟大的墙把ruby源给干掉了，可以把源换成淘宝提供的镜像，然后再次安装jekyll即可：

    gem sources -a http://ruby.taobao.org/
    gem install jekyll

# 然后安装[Markdown](http://wowubuntu.com/markdown/)的解析引擎，我个人喜欢用rdiscount。

    gem install rdiscount

# 最后，如果你想换用[Textile](http://redcloth.org/textile/writing-paragraph-text/)标记语言，那么你还需要安装RedCloth:

    gem install RedCloth

选择模板配置网站
----------------

------------------------------------------------------------------------

# 这步骤因人而异，我用的是[jekyllbootstrap](http://jekyllbootstrap.com/)，你也可以选择自己喜欢的模板，或者自己建一个([网络上找到的教程](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html))。下面我还是用jekyllbootstrap作为例子。

# 根据[QuickStart](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)的提示将模板的代码clone下来并设置为你的git仓库的URL。

# 修改代码根目录下的**_config.yml**文件，将你的站点和个人信息更新进去，同时在最后加上

    markdown: rdiscount

# 如果你用的是Textile，那么还要修改[*Rakefile*文件，将

    'post_ext' => "md"

修改为

    'post_ext' => "textile"

# jekyllbootstrap还提供了一些可供选择的主题模板，可以根据个人喜好更换

# 如果需要修改模板，可以在以下路径找到

    .assetsthemesbootstrap-3

语法高亮插件google-code-prettify
--------------------------------

------------------------------------------------------------------------

# 使用方法很简单，可以参考[官网教程](https://code.google.com/p/google-code-prettify/wiki/GettingStarted)。

# 这里重点说下偷懒的方法，每个pre标签都去添加class是件很费事的事情，由于我很懒，所以就直接用JQuery在模板里面添加代码，在页面加载完成后给所有pre标签加上**class="prettyprint"**。

    $(document).ready(function () {
        $("pre").addClass("prettyprint linenums");
    });

上面的代码前后要加上script标签。

分享和评论
----------

------------------------------------------------------------------------

1.  jekyllbootstrap原生支持disqus，但是国内的网络你懂的，所以还是找个国内的评论提供商靠谱点。
2.  右边栏分享我用的是[JiaThis](http://www.jiathis.com/)，评论功能则采用[友言](http://www.uyan.cc/)。
3.  使用方法直接看官网教程，非常简单，这里就不赘述了。

总结
----

------------------------------------------------------------------------

都完成之后，将代码提交并推送到GitHub上，通过username.github.io这个域名就可以访问到你的网站了（第一次提交可能要等十分钟才会生效）。
到此为止，基本上一个个人博客网站的大部分功能都齐全了，剩下的就是编写文章啦，这个我就不多说了，祝你玩得开心<sup>_</sup>。
