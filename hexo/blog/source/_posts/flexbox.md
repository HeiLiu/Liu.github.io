---
title: Css3之Flex布局
date: 2018-5-2
tags: 'Flex'
categories: 前端
---
## Flex(flexible box)  弹性布局
传统的布局解决方案，基于盒模型，通过 `css`中的`display`属性 + `position`属性 + `float`属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。 

+ 概念
    - 任何容器都可以设为`flex`布局
    - 采用flex布局的元素即为flex container，其子元素为容器成员(flex item)
    - 设为flex布局以后，子元素的float/clear/vertical-align属性将会失效  
+ 主轴和交叉轴  
    - **容器默认存在水平主轴`main axis`和垂直的交叉轴`cross axis`**
    - **flex-item排列的方向是主轴**      
+ `flex-container`容器属性  
    - **`flex-direction`决定主轴的方向(同时也是flex-item的排列方向)**
         > flex-direction: row | row-reverse | column | column-reverse; 
    
         - `row`（默认值）：主轴是水平方向，flex-item水平从左往右排列  
         - `column` : 主轴呈垂直方向,从上边沿向下排列  
         - `reverse`参数: 将起始与终点进行互换
    - `flex-wrap` 属性定义如果在一条轴线上排不下，换行的规则 
         >   flex-wrap：nowrap | wrap | wrap-reverse  
         - `nowrap`（默认值）：不换行
         - `wrap` : 自然换行 直接将多余的元素从下一行开始排列  
         - `wrap-reverse`: 将第一行排列到下方 
    - `flex-flow`  是`flex-direction`和`flex-wrap`的简写，默认值为`row` `nowrap`
    - `justify-content`:定义flex-item在主轴`main-axis`上的对齐方式     
        > justify-content: flex-start | flex-end | center | space-between | space-around   
        - `flex-start`（默认值）：左对齐；  
        - `flex-end`右对齐；  
        - `center`居中；
        - `space-between`：两端对其，flex-item间的间隔距离相等
        - `space-around`：每个flex-item两侧的间隔相等，相当于设置左右`margin`值相等
    - `align-items `: 定义`flex-item`在交叉轴的对齐方式
        > align-items: flex-start | flex-end | center | baseline | strecth。五个取值与交叉轴方向有关
        - flex-start|flex-end|center和flex-direction一样，只不过是在交叉轴起点、终点、中点对齐；
        - baseline：flex-item的第一行文字的基线对齐
        - stretch（默认值）：如果flex-item没有设置高度或者值为auto，将占满整个容器高度 
    - align-content：如果容器内出现多跟轴线（即出现wrap），定义主轴在交叉轴上的对齐方式，只有一根轴线时不起作用
        > align-content: flex-start | flex-end | center | space-between | space-around | stretch
       - `stretch`（默认值）：轴线沾满整个交叉轴
       - `space-between`：与交叉轴两端对齐，轴线间的间隔平均分布
       - `space-around`：每根轴线两侧的间隔相等
       - `flex-start`：与交叉轴起点对其  

+ `flex-item`项目的属性   
    - order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
    - flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大.<br/>
    &nbsp; &nbsp; &nbsp;如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
    - flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。负值对该属性无效。
    - flex 属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
        > flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    - flex-basis
    - align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。 
        > align-self: auto | flex-start | flex-end | center | baseline | stretch; 

