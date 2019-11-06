---
title: Axios
date: 2019-08-15
tags: 前端
categories:
  - Skill
  - JavaScript
---

## 先从fetch讲起  

一个简单的fetch例子如下：

```js
fetch('./api/person.json')
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      // 将返回数据 Json 化
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });

  1. .json()返回一个被解析为JSON格式的`promise`对象，当获取成功时，我们使用 json() 读取并解析数据

```
<!-- more -->
### 使用async/await简化  

由于Fetch底层是用Promise实现，我们可以直接用async来优化上面的代码，减少回调，使其更加语义化、容易理解， 代码如下：

```js
async function geturl(){
	try{
		let res = await fetch('./api/some.json')
		if(res.status == 200){
			console.log(await res.text())
		}
	} catch(err){
		console.log(err)
	}
}

```

```js
// response 其他返回数据
fetch('users.json').then(function(response) {
    console.log(response.headers.get('Content-Type'));
    console.log(response.headers.get('Date'));

    console.log(response.status);
    console.log(response.statusText);
    console.log(response.type);
    console.log(response.url);
});
```

#### Response 类型

当我们发起一个Fetch请求时，返回的response响应会自带一个response.type属性（basic、cors、opaque）。response.type属性说明了异步资源的来源，同时还有相应的处理方式。
当我们发起一个同源请求时，response.type为basic，而且你可以从response读取全部信息。  
如果我们访问一个非同源域名，并且有返回相应的CORs响应头时，那么该请求类型是cors。  cors和basic很相似，就除了cors响应里你无法访问Cache-Control，Content-Language，Content-Type，Expires，Last-Modified和Pragma
当我们对一个不同源的域名发起请求时，如果返回的响应头部没有CORS信息，那么这个response对应的类型就是opaque类型。一个opaque响应是无法读取返回的数据、状态，甚至无法确定这个请求是否成功。  
我们可以自定义Fetch请求的模式，要求返回对应类型的响应，有以下几种响应：

- 1.same-origin 只返回同源请求，其他类型会被reject  
- 2.cors 接收同源、非同源请求，返回有CORs头部的响应  
- 3.cors-with-forced-preflight 在发出请求前会先做一次安全性检查  
- 4.no-cors 用来发起没有CORS头部并且非同源请求，并且会返回opaque响应。但是目前这种类型只能在Service Worker里使用，在window.fetch里不能用  

### POST请求类型  

使用Fetch发起Post请求时，需要手动设置method参数和body参数，如下：  
```js
fetch(url, {
    method: 'post',
    headers: {
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
    },
    body: 'foo=bar&lorem=ipsum'
  })
  .then(json)
  .then(function (data) {
    console.log('Request succeeded with JSON response', data);
  })
  .catch(function (error) {
    console.log('Request failed', error);
  });

```

###  带 COOKIE 发送请求  

在异步请求中带上cookie参数，那么需要显式指定credentials参数：

```js
fetch(url, {
  credentials: 'include'
})
```
## Axios

Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。

### 特性

- 从浏览器中创建 XMLHttpRequests  
- 从 node.js 创建 http 请求  
- 支持 Promise API  
- 拦截请求和响应  
- 转换请求数据和响应数据  
- 取消请求  
- 自动转换 JSON 数据  
- 客户端支持防御 XSRF  

### 安装

npm 安装：  
```
  $ npm install axios
```
使用cdn:  
```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### GET 请求

### POST 请求  

### 响应结构  

响应返回包含信息：  
```js
{
  // `data` 由服务器提供的响应
  data: {},

  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',

  // `headers` 服务器响应的头
  headers: {},

  // `config` 是为请求提供的配置信息
  config: {}
}
```


[文档传送门](https://www.kancloud.cn/yunye/axios/234845)