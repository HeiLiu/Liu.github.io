---
title: js基本数据类型和引用类型的区别
date: 2018-07-30 15:01:13
tags: 'javascript'
categories: 前端
copyright: true
---
 

## Js 基本数据类型  

js基本数据类型包括：undefined,null,number,boolean,string.基本数据类型是按值访问的，就是说我们可以操作保存在变量中的实际的值  

### 1.基本数据类型的值是不可改变的  
 任何方法都无法改变一个基本类型的值是不可改变的，比如一个字符串：  
 ```js
  var name = "change";
  name.substr();//hang
  console.log(name);//change

  var s = "hello";
  s.toUpperCase()//HELLO;
  console.log(s)//hello  

 ```

 通过这两个例子， 我们原来发现定义的变量name 的值始终没有发生改变，而调用substr() 和 toUpperCase() 方法后返回的是一个新的字符串，跟原先定义的变量name 并没有关系  

 或许有人会有一下的疑问， 看代码：   

