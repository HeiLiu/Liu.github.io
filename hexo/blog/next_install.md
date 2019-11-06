---
title: 在hexo中安装next主题  
date: 2018-04-25
tags: '倒腾'
categories: hexo
---

----------
    倒腾了一天半终于自己实现了一个还不错的博客，在这篇文章中，假定你已经成功安装了 Hexo，并使用 Hexo 提供的命令创建了一个站点。如果没有搭建好自己的hexo+git pages博客界面可以看我另外一篇经验分享
    
    **说明**：在 Hexo 中有两份主要的配置文件，其名称都是 _config.yml。 其中，一份位于站点根目录下，主要包含 Hexo本身的配置；另一份位于主题next目录下，这份配置由主题作者提供，主要用于配置主题相关的选项。为了描述方便，在以下说明中，将前者称为 站点配置文件， 后者称为 主题配置文件。  
    
---

 - 下载主题 
    - 下载方式：
    

    1.在theme文件夹中将主题包克隆到本地，并将文件名`hexo-theme-next`改成`next`  
            git clone https://github.com/iissnan/hexo-theme-next themes/next
        2.前往Next[发布页面][1]将`sourcecode`下载到本地，解压所下载的压缩包至站点的 themes 目录下， 并将 解压后的文件夹名称（`hexo-theme-next-0.4.0`）更改为 `next`。
        
    
 - 启用Next  
        当 克隆/下载 完成后，打开 站点配置文件， 找到 `theme` 字段，并将其值更改为`next`。

 - 验证主题是否应用
       1. NexT 主题安装完成。下一步我们将验证主题是否正确启用。在切换主题之后、验证之前， 最好使用 `hexo clean` 来清除 Hexo 的缓存。
       2. 执行`hexo generate` 生成博客
       3. 执行`hexo server`启用本地服务器 在本地可以直接查看修改以后的效果
            >`INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to`  
            使用浏览器进行访问http://0.0.0.0:4000/
 

 - 修改主题样式scheme
    Scheme 的切换通过更改 主题配置文件，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 # 去除即可。
    

>  #Schemes
    #scheme: Mist
    scheme: Muse
    #scheme: Pisces
    #scheme: Gemini

 - 其他基本配置  
    打开`站点配置文件` 可以像我一样进行基本设置 `每个冒号后面必须与内容用空格分割`

>  #Site
title: HeiLiu //站点title
subtitle: 有一句Hello World想要对你说
description: 程序员 大学本科
keywords:
author: 刘江龙
language: zh-Hans   //设置语言
timezone: Asia/Shanghai  //时间
> 
>  #Deployment
 ## Docs: https://hexo.io/docs/deployment.html
deploy: 
  type: git
  repo: https://github.com/HeiLiu/HeiLiu.github.io.git
  branch: master



   
       
        


  [1]: https://github.com/iissnan/hexo-theme-next/releases