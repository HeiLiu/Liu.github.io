---
title: 自己搭建博客
date: 2018-04-19 21:46:12
tags: '倒腾'
categories: hexo
---
#### Hexo 是开源的npm的博客包
	使用markdown语法写博客 结合github page 服务，有一个免费的开源博客
  + git配置过程  
 
       - 全局配置 username email ssh
            在git bash中执行代码：  
                1. git config global user.name "gitname"  
                2.git config global user.email "email"  
                3.ssh-keygen -t rsa -C "git@email"  一路回车  
            找到.ssh文件夹 打开id_rsa.pub复制内容   
                4.到github上 setting 中ssh key添加 title为空 粘贴ssh至内容中  
       - 验证一下是否成功  
            1.在hexo目录下将  
            https://github.com/HeiLiu/HeiLiu.github.io.git
                

  + hexo init 初始化博客  

      1.  执行一下初始化命令系统会去github clone一个博客来到本地  
       2. ./node_modules是以来文件夹，npm包 项目所有依赖都在这里。  
        3.博客存放地址 source/_post/**.md
        4.markdown 语法 更简捷的写html  
        5.theme主题文件夹

  +  hexo clean 
       - 清空生成的站点博客文件  
            
  + hexo generate  
       - 博客的产生  
            hexo generate 将markdown语法编译成public/*.html
  + hexo server  
        打开本地服务器  

  + hexo deploy
      - 将本地生成的public文件内容发布到github      
