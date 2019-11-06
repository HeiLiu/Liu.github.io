---
title: JS对数组去重的几种方法
date: 2018-04-22 22:11:49
tags:
  - 🌝 
  - 面试
  - JavaScript
---

面试经常问的一道题
**JS对数组去重的几种方法 (前面六种方法是普通数组，最后一种是对象数组)**


<!-- more -->
<font color=black size=4>**方法一：**</font> 最原始的方法，定义一个新数组，并存放原数组的第一个元素，然后将元素组一一和新数组的元素对比，若不同则存放在新数组中。
``` javascript 
  var arr = [ 1, 1, '1', '1'];
  function uniqueArr(oldArr) {
    // 新的数组 用来存放去重后的值
    var newArr = [];  
    for (var i = 0; i < oldArr.length ;i++) {
      for (var j = 0 ; j < newArr.length; j++) 
        // 如果两数相等 则跳出第二个循环
        if (oldArr[i] === newArr[j]) break; 
      // 一轮循环结束还没跳出循环 则表示此数未再新数组里出现 则加入新数组 
      if (j == newArr.length)  newArr.push(oldArr[i]);   
    }
    return newArr;
  }
  console.log(uniqueArr(arr));  // [ 1, '1' ]
```

<font color=black size=4>**方法二：**</font> 先将数组排序，再相邻的进行比较，不同的存入新数组。（这个方法有缺陷，因为sort是按照字符编码的顺序进行排序，所以要先将数组的元素转换为字符串，来进行比较，下面的数组的这种情况就不能完美的去重。 **个人认为sort方法是通过交换实现的排序，在数据量比较小的时候用的是冒泡排序，数据量比较大时用的是快速排序**）
``` javascript
  var arr = [ 1, 1, '1', '1', 1];
  function uniqueArr(oldArr) {
    oldArr = oldArr.sort(); 
    var newArr = [];
    for (var i = 0 ; i < oldArr.length ; i++) {
      if(oldArr[i] !== newArr[newArr.length-1])
        newArr.push(oldArr[i]);
    }
    return newArr;
  }
  console.log(uniqueArr(arr));  // [ 1, '1', 1 ]
```

<font color=black size=4>**方法三：**</font> 利用数组的indexOf下标属性来简化循环 (includes 也是一样的)
``` javascript
  var arr = [ 1, 1, '1', '1', 1];
  function uniqueArr(oldArr) {
    var newArr = [];
    for (var i = 0 ; i < oldArr.length ; i++) 
      //  利用indexof 判断某个值是否在新的数组里面
      if(newArr.indexOf(oldArr[i]) === -1) 
        newArr.push(oldArr[i]);
    return newArr;
  }
  console.log(uniqueArr(arr));   // [ 1, '1' ]
```

<font color=black size=4>**方法四：**</font> 利用ES6的 filter 方法 加上indexOf 返回第一个item出现的位置
``` javascript
  var arr = [ 1, 1, '1', '1', 1, '2'];
  function uniqueArr(oldArr) {
    var newArr = oldArr.filter(function(item, index, oldArr){
      // indexOf 返回第一个item出现的位置 
      return oldArr.indexOf(item) === index;
    })
    return newArr;
  }
  console.log(uniqueArr(arr));  // [ 1, '1', '2' ]
```

<font color=black size=4>**方法五：**</font> 利用对象属性存在的特性，如果没有该属性则存入新数组 (这里的 1 和 ‘1’ 在用obj[]添加属性时，会被自动换成 1 然后加入进obj)
``` javascript 
  var arr = [ 1, 1, '1', '1', 1, '2'];
  function uniqueArr(oldArr) {
    var newArr = [];
    var obj = {};
    for(var i=0; i<oldArr.length; i++){
      if( !obj[oldArr[i]] ){
        // 属性不存在 则加入新数组 并将该属性变为 1
        obj[oldArr[i]] = 1;
        newArr.push(oldArr[i]);
      }
    } 
    return newArr;
  }
  console.log(uniqueArr(arr));   // [ 1, '2' ]
```

<font color=black size=4>**方法六：**</font>利用ES6的 set 对象自动去重
``` javascript
  var arr = [ 1, 1, '1', '1', 1];
  function uniqueArr(arr) {
    return Array.from(new Set(arr));  // 利用Array.from 将Set结构转换为数组
  }
  console.log(uniqueArr(arr));   // [ 1, '1' ]
```

<br>
<font color=black size=5>Object键值对去重</font>
``` javascript 
  var arr = [{value: 1}, {value: 1}, {value: 2}];
  function uniqueArr(oldArr) {
    var obj = {};
    return oldArr.filter(function(item, index, oldArr){
      // 判断 obj 对象是否存在item这个属性  存在的话返回fasle 不存在的话 向Obj中添加该属性
      return obj.hasOwnProperty(typeof item + JSON.stringify(item)) ? false : (obj[typeof item + JSON.stringify(item)] = true)
    })
  }
  console.log(uniqueArr(arr));   // [{value: 1}, {value: 2}]
```
