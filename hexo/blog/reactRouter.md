---
title: React-router V4
date: 2019-08-21
tag: React-router
categories: 
  - React
---

React 创建的单页应用中、通过路由来控制页面间的跳转，常用的就是 react-router、react-router-dom

# React Router中有三类组件

- 路由组件 BrowserRouter, HashRouter  
- 路由匹配组件 Route, Switch  
- 导航、链接组件 Link

> 基于 React Router 的 web 应用，根组件应该是一个 router 组件（BrowserRouter，HashRouter ）。 项目中，react-router-dom 提供了和两种路由。两种路由都会创建一个 history 对象。如果我们的应用有服务器响应 web 的请求，我们通常使用<BrowserRouter/>组件; 如果使用静态文件服务器，则我们应该使用<HashRouter/>组件  通常都是使用 <BrowserRouter/>


## Demo  

Link 组件最终会渲染为 HTML 标签 <a>，它的 to、query、hash 属性会被组合在一起并渲染为 href 属性。虽然 Link 被渲染为超链接，但在内部实现上使用脚本拦截了浏览器的默认行为，然后调用了history.pushState 方法