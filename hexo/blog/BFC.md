---
title: BFC 浅谈
date:
tags: 'css'
categories: 前端
---

## 写在前面

------   
> Block formatting context （块级格式化上下文）  

页面文档由块`block`构成 每个`block`在页面上占据自己的位置  
使用新的元素构建BFC overflow：hidden | auto | scroll； 只要不为`visible `新的空间  
告诉浏览器，外面的环境影响不到我了 我重新来进行Block formatting 布局和定位  

**核心：**  
    新的BFC，给出了新的不受外界影响的块级格式化环境  
    block 块级-> 页面的基础  
    formatting context 格式化-> 渲染
    
### 浏览器构建文档树的时候 布局和定位元素  
网页的定位（大） 文档流正常，浮动，定位，flex，table
广义的定位 块级元素的定位 垂直的定位；行内元素 左右定位 通过内容来确定  
狭义的定位：
float 浮动元素，在一行的开始或者结束  
flex 弹性布局 
position

BFC 在正常的文档流里面重建一个新的上下文环境  

### BFC的约束规则  
- 一、在浏览器进行页面元素布局的时候 同一个BFC的两个相邻的Box的margin 会重叠，与方向无关  
    > 破坏规则 创建新的BFC Context上下文的概念   

    如何创建BFC？=>重新规划一个（独立）渲染区域
    + 根元素body，天然是一个BFC    
    + overflow:hidden;  
    + float 不为none  
    + display:inline-block | table-cell |table-caption  
    + position:absolute | fixed 只要不为static  
    > 好像只剩块级元素和行内元素不是BFC
    
- 二、`BFC`的高度，浮动元素也要参与计算  
   > 在元素`float `之后脱离了文档流没有办法计算确切高度，这种情况我们称之为高度塌陷。解决高度塌陷的前提就是`能识`别并`包含`到浮动元素。**而`BFC`就有这个特性**，所以BFC也可以计算浮动元素的高度。新建BFC让浮动元素也参与计算 
```html
    <style>
        *{padding: 0;margin: 0;}
        .par{
            border: 5px solid #fcc;
            width: 300px;
            /*这里的overflow并不是为了超出则隐藏，而是为了创建一个BFC*/
            /* overflow: hidden; */
            display: inline-block;
        }
        .child{
            border: 5px solid #f66;  
            width: 100px;
            height: 100px;
            float: left;
            /* clear: both; */
        }
    </style>
</head>
<body>
    <!-- 网页的定位（大） 文档流正常，浮动，定位，flex，table -->
    <div class="par">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</body>
```  
- 三、每个元素的左边，要与包含盒子的左边相接触
- 四、BFC的区域不会与float box重叠  
```html
    <style>
        *{padding: 0;margin: 0;}
        .aside{
            float: left;
            width: 100px;
            height: 150px;
            background-color: #ff6666;
        }
        .main{
            height: 200px;
            background: #ffcccc;
            /* clear: left; */
            overflow: hidden;
        }
    </style>
</head>
<body>
    <!-- 自适应两栏式布局 类似于flex：1；
    aside 和 main 处于同一BFC（body）下 
    BFC布局规则3 规则4 -->
    <div class="aside"></div>
    <div class="main"></div>
</body>
```   
```html
/*BFC在三栏式布局中的应用*/
    <style>
        *{padding: 0;margin: 0;}
        .container{
            height: 200px;
        }
        .left,.right,.center{
            height: 200px;
        }
        .left{
            background: pink;
            float: left;
            width: 180px;
        }
        .right{
            background: lightblue;
            width: 180px;
            float: right;
        }
        .center{
            background: yellow;
            overflow: hidden;
        }
    </style>
</head>
<body>
    <!-- 三栏式布局 -->
    <div class="container">
        <!-- 页面的结构与呈现效果不一致？想一下 -->
        <div class="left">Left</div>
        <div class="right">Right</div>
        <div class="center">Center</div>
    </div>
</body>
```  

**注意：**  
> 通过 overflow:hidden将元素转换为BFC，固然可以解决高度塌陷的问题，但是大范围的应用在布局上是肯定是行不通的，毕竟overflow会造成溢出隐藏的问题，特别是与JS交互的效果时。  

那有没有一个更好的高度检测方法呢？
答案是有的，就是我们经常用到的clearfix。  
```css
.clearfix:after{
    content:'';
    display:table;
    clear:both
}
.clearfix{
    *zoom:1;/* IE6,7不支持BFC，所以需要通过专有的CSS属性，触发hasLayout。*/
}
```
[关于zoom:1][1]


  [1]: https://www.cnblogs.com/meierbao/p/6526247.html