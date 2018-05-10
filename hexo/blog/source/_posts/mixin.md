---
title: stylus之变量与mixin
date:
tags: 'Css'
categories: 前端
---

## 混合书写(Mixins)  

------  
### 变量
- 在`stylus`中 可以将常用的样式像表达式中变量赋值一样保存给一个变量、如下：
```css
    /*进行变量的声明*/
    bg_color = #123456;
    box_size = 100px;
    /* 使用 */
    .box
        background-color bg_color
        width box_size
        height box_size
```
    编译后：
```css
 .box {
    background-color: #123456;
    width: 100px;
    height: 100px;
    }
```
- 属性查找  
Stylus有另外一个很酷的独特功能，不需要分配值给变量就可以定义引用属性。下面是个很好的例子，元素水平垂直居中对齐（典型的方法是使用百分比和margin负值），如下：
```css
    #logo
        position: absolute
        top: 50%
        left: 50%
        width: w = 150px
        height: h = 80px
        margin-left: -(w / 2)
        margin-top: -(h / 2)
```
在`stylus`中可以不使用这里的变量w和h, 而是简单地前置`@`字符在属性名前来访问该属性名对应的值：
```css
    #logo
        position: absolute
        top: 50%
        left: 50%
        width: 150px
        height: 80px
        margin-left: -(@width / 2)
        margin-top: -(@height / 2)
```
### 混合书写
- 混合书写和函数定义方法一致，但是应用却大相径庭。

例如，在书写`Css3`样式时我们经常要进行兼容性处理，需要在属性前加上相应的前缀，下面有定义的border-radius(n)方法，其却作为一个mixin（如，作为状态调用，而非表达式）调用。   
```css
    bg_color = #123456;
    box_size = 100px;

    /*定义mixin*/
    border-radius(n)
        -webkit-border-radius n
        -moz-border-radius n
        -ms-border-radius n
        -o-border-radius n
        border-radius n
    .box
        background-color bg_color
        width box_size
        height box_size
        border-radius(5px)
```  
进一步，我们可以利用arguments这个局部变量，传递可以包含多值的表达式,这样就可以給属性传递多个值。  
```css
border-radius()
        -webkit-border-radius arguments
        -moz-border-radius arguments
        -ms-border-radius arguments
        -o-border-radius arguments
        border-radius arguments
```
`Stylus`支持通过使用{}字符包围表达式来插入值，其会变成标识符的一部分。例如，-webkit-{'border' + '-radius'}等同于`-webkit-border-radius`. 
 
再进一步，在stylus中我们还可以对border-radius再做进一步的处理 类似与js中的函数封装 ，如下(这样对于任何需要做兼容性处理的属性 我们只需要调用两次mixin出入所需参数，大大的简化了一下琐碎代码工作): 
 ```css
 vendor(prop,args)
    -webkit-{prop} args
    -moz-{prop} args
    -ms-{prop} args
    -o-{prop} args
    {prop} args

border-radius(n)
    vendor('border-radius',arguments)
box-shadow(n)
    vendor('boa-shadow',arguments)
.box
    background-color bg_color
    width box_size
    height box_size
    border-radius(5px)
 ```
 编译后：
 ```css
 .box {
  background-color: #123456;
  width: 100px;
  height: 100px;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -o-border-radius: 5px;
  border-radius: 5px;
  -webkit-box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
  -moz-box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
  -ms-box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
  -o-box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
  box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
}
 ```

