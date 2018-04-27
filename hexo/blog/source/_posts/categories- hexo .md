---
title: next主题个性化配置  
date: 
tags: '倒腾'
categories: hexo
---

> 看到一些大神的next博客站点很酷 那到底是怎么实现的呢 经过一番的倒腾，终于将一些使用且比较酷的功能添加到自己的博客中  

### 主要添加的功能有：

 - 在右上角或者左上角实现fork me on github
 - 添加RSS·
 - 添加动态背景·
 - 在每篇文章末尾统一添加“本文结束”标记
 - 修改作者头像并旋转
 - 主页文章添加阴影效果
 - 在网站底部加上访问量
 - 添加菜单分类页面·
 - 网站底部字数统计
 - 添加 README.md 文件·
 - 隐藏网页底部powered By Hexo / 强力驱动
 - 添加来必力评论 Livere·
 - DaoVoice 在线联系
 - 添加站内搜索
#### **实现fork me on github**

#### **1.修改头像并配置头像样式**
- 编辑 ·主题配置文件·， 修改字段 `avatar， 值设置成头像的链接地址。其中，头像的链接地址可以是：  
    > 将头像图片放置在 source/images/ 目录下 
        配置为：avatar: /images/avatar.png
        或者使用图片的在线地址
#### **2.设置博客背景动画**
NexT 自带两种背景动画效果：
编辑 主题配置文件， 搜索 canvas_nest 或 three_waves，根据您的需求设置值为 true 或者 false 即可：如下、
>  #canvas_nest
    canvas_nest: true //开启动画
        

>   # three_waves
    three_waves: false //关闭动画
    
#### **3.添加RSS**
在blog目录下安装hexo-generate-feed  然后打开z主题配置文件,在里面配置为如下样子：(就是在rss:的后面加上/atom.xml,注意在冒号后面要加一个空格)
>   #Set rss to false to disable feed link.
    #Leave rss as empty to use site's feed link.
    # Set rss to specific value if you have burned your feed already.
    rss: /atom.xml
    
####**4.在网站底部加上访问量**
    > 啊但是发射点法
    
#### **5.网站底部字数统计**  

&nbsp; 修改如下部分

>   # Post wordcount display settings
    # Dependencies: https://github.com/willin/hexo-wordcount
    post_wordcount:
      item_text: true
     wordcount: true
    min2read: true
    totalcount: false
     separated_meta: true  
     
在适当的位置添加以下页面代码

####**6.添加README.md**
- 每个项目下一般都有一个 README.md 文件，但是使用 hexo 部署到仓库后，项目下是没有  README.md 文件的。

- 在 Hexo 目录下的 source 根目录下添加一个 README.md 文件，修改站点配置文件 _config.yml，将 skip_render 参数的值设置为`skip_render:README.md`
- 保存退出即可。再次使用 hexo d 命令部署博客的时候就不会在渲染 README.md 这个文件了。
#### 添加菜单分类/标签页面
&nbsp;  在hexo站点目录下 使用`hexo new page` 新建一个页面 命名为tags 如下：
 >   hexo new page tags  
    此时会在hexo > source文件夹中会生成一个`tags`文件夹。
    编辑tags文件夹下面的`.md`文件

  &nbsp;   在菜单中添加链接。编辑 主题配置文件 ， 添加 tags 到 menu 中，如下:
> menu:
  home:  / || home
  archives:  /archives/ || archive
  tags:  /tags/ || tags
  
 &nbsp; 注：||之前的值是`目标链接`，之后的是页面的`图标`，图标名称来自于FontAwesome icon。若没有配置图标，默认会使用问号图标。

#### **7.添加livere来必力评论模块**
**注意**：最新版 hexo-theme-next 已经包含 LiveRe 插件，下载`最新版本`，配置 `livere_uid` 即可使用

##### **获取livere_uid步骤**

 1. 注册 LiveRe

> 进入 LiveRe，注册账号。
> 
> LiveRe 有两个版本：
> 
> City 版：是一款适合所有人使用的免费版本；
Premium 版：是一款能够帮助企业实现自动化管理的多功能收费版本。City版就够了。
> 安装，获取 uid：

![此处输入图片的描述][1]
填写完成后，进入到 管理页面 -> 代码管理 -> 一般网站 代码中，`data-uid` 即为所需 `uid`

 2. 添加 LiveRe 插件

    第一步

    首先在 _config.yml 文件中添加如下配置：

    >  # Support for LiveRe comments system.
    >  # You can get your uid from https://livere.com/insight/myCode (General web site)
    livere_uid: your uid

    其中 livere_uid 即上一步获取到的 uid。其他的设置在最新版中都不需要配置啦 所以说程序员还是要用新的潮的东西**？有个地方还要试试**
    
#### **8.设置网站图标**
 具体方法实现

    找一张（32*32）的ico图标，并将图标名称改为favicon.ico，然后把图标放在/theme    s/next/source/images里，并且修改`主题配置文件`,下面就是图标配置代码修改即可：

> favicon: 
  `small: /images/favicon-16x16-next.png`
  `medium: /images/favicon-32x32-next.png`
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg

#### **9.站内博客搜索**  

添加百度/谷歌/本地 自定义站点内容搜索.

    1.安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：  
    
  >  npm install hexo-generator-searchdb --save
    
    
    2.编辑 站点配置文件，新增以下内容到任意位置：
    
  > search:
      path: search.xml
      field: post
      format: html
      limit: 10000
      
3.编辑 主题配置文件，启用本地搜索功能：
    >   #Local search
         local_search:
        enable: true



  [1]: https://blog.smoker.cc/images/web/livere-get-code.png