---
title: 在 React 中使用 mobx 进行状态管理
date: 2019-10-14
tag: React
categories: Note
---

observable 
inject 
computed 
action 

RunInAction 
Reaction 

调试

toJs 需要引入 => 不如直接 JSON.stringify()方便

不用使用数组索引或者任何将来可能会改变的值作为 key 。如果需要的话为你的对象生成 ids。

[参考技巧](https://cn.mobx.js.org/best/react-performance.html)

<!-- 中文排序 -->

```js 
var array = [{name:'武汉'}, {name: '北京'}, {name:'上海'}, {name:'天津'}];
var resultArray = array.sort(
    function compareFunction(param1, param2) {
        return param1.name.localeCompare(param2.name,"zh");
    }
);
console.log(resultArray);
```
