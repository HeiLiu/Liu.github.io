---
title: E2E 测试
date: 2019-08-14
tag: test
categories:
  - test
---

# 测试

[参考链接](https://segmentfault.com/a/1190000015724775)  

## 小程序自动化  
小程序自动化SDK为开发者提供了一套通过外部脚本操控小程序的方案，从而实现小程序自动化测试的目的。  

通过该 SDK，你可以做到以下事情：

- 控制小程序跳转到指定页面  
- 获取小程序页面数据  
- 获取小程序页面元素状态  
- 触发小程序元素绑定事件  
- 往 AppService 注入代码片段  
- 调用 wx 对象上任意接口  

安装小程序自动化SDK：  
```js
npm install miniprogram-automator --save-dev
```
