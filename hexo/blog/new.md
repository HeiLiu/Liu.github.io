---
title: 如何手动实现一个New操作
date:
tags: JavaScript
categories: 前端
---

## 写在前面

------   
在所有的前端面试中常常喜欢考面试者如何手写一个new操作符，作为在准备秋招的大三党，我也要考虑这些。
那么我们先看看new操作符都干了什么事情，有哪些操作？通过下面的代码来进行思考：  
```js
// 新建一个类（构造函数）
function Otaku(name, age) {
    this.name = name;
    this.age = age;
    // 自身的属性
    this.habit = 'pk';
}
// 给类的原型上添加属性和方法
Otaku.prototype.strength = 60;
Otaku.prototype.sayYourName = function () {
    console.log('I am ' + this.name);
}
// 实例化一个person对象
const person = new Otaku('乔峰',5000);
person.sayYourName();
console.log(person);//打印出构造出来的实例
```    
![控制台打印结果](http://p9utic4op.bkt.clouddn.com/new.png)   


## 解析  

从控制台打印出来的结果我们可以看出new操作符大概做了一下几件事情：  

 1. 返回（产生）了一个新的对象  
 2. 访问到了类Otaku构造函数里的属性  
 3. 访问到Otaku原型上的属性和方法  并且设置了this的指向（指向新生成的实例对象）
 
通过上面的分析展示，可以知道new团伙里面一定有Object的参与，不然对象的产生就有点说不清了。 先来边写写：  

```js
// 需要返回一个对象 借助函数来实现new操作 
// 传入需要的参数： 类 + 属性
const person = new Otaku('乔峰',5000);
const person1 = objectFactory(Otaku, '鸠摩智', 5000);

// 开始来实现objectFactory 方法 
function objectFactory(obj, name, age) {}
// 这种方法将自身写死了 如此他只能构造以obj为原型，并且只有name 和 age 属性的 obj
// 在js中 函数因为arguments 使得函数参数的写法异常灵活，在函数内部可以通过arguments来获得函数的参数
function objectFactory() {
    console.log(arguements); //{ '0': [Function: Otaku], '1': '鸠摩智', '2': 5000 }
     // 通过arguments类数组打印出的结果，我们可以看到其中包含了构造函数以及我们调用objectfactory时传入的其他参数
    // 接下来就是要想如何得到其中这个构造函数和其他的参数
    // 由于arguments是类数组，没有直接的方法可以供其使用，我们可以有以下两种方法:
    // 1. Array.from(arguments).shift(); //转换成数组 使用数组的方法shift将第一项弹出
    // 2.[].shift().call(arguments); // 通过call() 让arguments能够借用shift方法
    const Constructor = [].shift.call(arguments);
    const args = arguments;
    // 新建一个空对象 纯洁无邪
    let obj = new Object();
    // 接下来的想法 给obj这个新生对象的原型指向它的构造函数的原型  
    // 给构造函数传入属性，注意：构造函数的this属性
    // 参数传进Constructor对obj的属性赋值，this要指向obj对象
    // 在Coustructor内部手动指定函数执行时的this 使用call、apply实现
    Constructor.call(obj,...args);
    return obj;
}

```  

- 上面的代码注释太多，剔除注释以后的代码：

```js
    function objectFactory() {
        let Constructor = [].shift.call(arguments);
        const obj = new Object();
        obj.__proto__ = Conctructor.prototype;
        Constructor.call(obj,...arguments);
        return obj;
    }
```    
- 还有另外一种操作： 

```js
function myNew(Obj,...args){
  var obj = Object.create(Obj.prototype);//使用指定的原型对象及其属性去创建一个新的对象
  Obj.apply(obj,args); // 绑定 this 到obj, 设置 obj 的属性
  return obj; // 返回实例
}
```

