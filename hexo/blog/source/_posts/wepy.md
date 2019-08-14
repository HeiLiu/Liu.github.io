---
title:  WePY  上手 
date: 
tags: '小程序'
categories: 小程序
---

# 来自微信官方的小程序组件开发框架 
## 介绍  
    WePY (发音: /'wepi/)是一款让小程序支持组件化开发的框架，通过预编译的手段让开发者可以选择自己喜欢的开发风格去开发小程序。  
- 类Vue开发风格
- 支持自定义组件开发
- 支持引入NPM包
- 支持Promise
- 支持ES2015+特性，如Async Functions
- 支持多种编译器，Less/Sass/Stylus/PostCSS、Babel/Typescript、Pug
- 支持多种插件处理，文件压缩，图片压缩，内容替换等
- 支持 Sourcemap，ESLint等
- 小程序细节优化，如请求列队，事件优化等

## 安装使用  
### 安装（更新）wepy命令行工具  
```js
npm install wepy-cli -g
```
### 生成开发实例  
```js
npm init standard projectName
```  
生成src的目录 开发在此目录进行开发
### 安装依赖  
```js
npm install
```  
将所有项目和开发时（package.json）所需要的依赖进行安装
### 开启实时编译
```js
wepy build --watch
```  
生成dist目录、并实时监听src目录下的修改且编译到dist目录中     
### WePY项目目录结构

```
>├── dist                   小程序运行代码目录（该目录由WePY的build指令自动编译生成，请不要直接修改该目录下的文件）
├── node_modules           
├── src                    代码编写的目录（该目录为使用WePY后的开发目录）
|   ├── components       WePY组件目录（组件不属于完整页面，仅供完整页面或其他组件引用）
|   |   ├── com_a.wpy      可复用的WePY组件a
|   |   └── com_b.wpy      可复用的WePY组件b
|   ├── pages              WePY页面目录（属于完整页面）
|   |   ├── index.wpy      index页面（经build后，会在dist目录下的pages目录生成index.js、index.json、index.wxml和index.wxss文件）
|   |   └── other.wpy      other页面（经build后，会在dist目录下的pages目录生成other.js、other.json、other.wxml和other.wxss文件）
|        └── app.wpy            小程序配置项（全局数据、样式、声明钩子等；经build后，会在dist目录下生成app.js、app.json和app.wxss文件）
└── package.json           项目的package配置
```
### 开发者工具导入项目  
使用微信开发者工具新建项目，本地开发选择生成的dist目录，会自动导入项目目录配置  

[WePY官方文档][1]


  [1]: https://tencent.github.io/wepy/document.html#/