---
title: 【轻松集赞】写了个涉嫌混淆微信官方服务的小程序
date:
tags: '小程序'
categories: 小程序
---

------
 
![此处输入图片的描述][1]  
### 发生背景：
&nbsp;&nbsp;&nbsp;&nbsp;随着现在国内的社交软件用户群体的不断扩大，商家打广告的方式（套路）也越来越多了，每次走在大街上都可以看到商家打出来广告牌，"朋友圈点赞超过30享受六折优惠"。在上一次和女盆友出去万达吃个晚饭，终于我们也被这个活动诱惑了一下下，作为口袋钱不多又想好好吃一顿的大三狗，看看望着桌子上一大盆烤鱼，还在犹豫要不要点一份小龙虾的女朋友，还是选择了拍照发朋友圈然后挨个去群里叫亲朋好友点赞，麻烦了一堆好友，真是不好意思。  
&nbsp;&nbsp;&nbsp;&nbsp;吃饱喝足，两个人扶着腰走在路上炫'腹'、还是女盆友的提醒说，你不是会小程序吗，能不能写一个点赞的小程序来用。哎、还真是，我自己撸一个，说不定还能给其他人用。  
### 初局雏形  
#### 分析了一下小程序要的功能：

     1. 主要功能：点赞（想要多少赞就要多少赞）  
     2. 微信朋友圈部分功能    
#### 项目结构   
感觉这个小程序比较适合想要练手小程序和WeUI的盆友，所以细讲一点
```
>├── assets 小程序所需的images icon                 
├── pages   页面目录          
|   ├── welcome 欢迎页面      
|   ├── index   内容发布操作页面
|   ├── mian   '朋友圈' 
├── style   页面的样式 及weui
└── app.js  小程序逻辑 全局参数
└── app.wxss 小程序公共样式
└── app.json   项目的配置
```
需要注意的地方：微信朋友圈发布一张图片和多张图片图片宽高比例不一样  
#### 欢迎页面Welcome  
欢迎页的动画我很喜欢，也许是这一个小程序的亮点
   ![此处输入图片的描述][2]  
   各位，请原谅我、我也不知道怎么就变成横向的了    
### 写在后面  

 1. 小程序在模拟器上实现一些复杂功能和界面效果时，及时在移动设备上进行效果查看，        避免移动端上达不到预期效果，ios和android有时候在样式的显示上有时也会有不同    
 2. 
  


  [1]: http://p9utic4op.bkt.clouddn.com/sx.png
  [2]: http://p9utic4op.bkt.clouddn.com/welcome_clip1.gif