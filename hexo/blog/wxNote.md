---
title: 微信小程序笔记总结
date:
tags: 'WXApp'
categories: 微信
---
---

### 小程序的项目架构  
- 基础组件 
- 地图
- 视图容器  
- 
### 组件   

### 事件   

### 数据绑定  

### template 只支持wxml wxss 模板 模块化不支持  

### wx:for wx:key wx:if   

### 样式导入 和 模块引入  

### 数据缓存  
    // 设置缓存 缓存是永久存在的 没有时效 上限最大不能超过10M
    // wx.setStorageSync ("collect", true);
    // 修改缓存，同名
    wx.setStorageSync('key',{
      game:"风暴英雄",
      developer:'暴雪'
    });
    // var postCollected=wx.getStorageSync("collected");
  },
  collectionTap(event){
    let game = wx.getStorageSync('key');
    console.log(game.developer);
  },
  shareTap(event){
    // wx.removeStorageSync('key');
    // 清除所有缓存
    wx.clearStorageSync();
  },



