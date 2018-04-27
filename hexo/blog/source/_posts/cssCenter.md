---
title: 让div在屏幕上居中（水平居中+垂直居中）的方法总结
date:
tags: 'Css'
categories: 前端
---
 - html代码如下：
 

    ```html
    <div class="book p3d">
            <div class="front-cover p3d">
                <div class="page front flip p3d">
                </div>
                <div class="page back"></div>
            </div>
    </div>
    ```  
 - Css居中方法 （敲黑板）重点  
    - 首先将元素设置成为`绝对定位`，然后`距顶部和左各50%`，此时的元素还不是居中的，因此需要`通过一定的偏移`将其移到理想位置，两种方法的`主要思想`都是一样的，第一种通过margin-left和margin-top`移动元素自身宽高的一半`，另一种通过`css3`的属性transform的`translate方法`平移元素自身宽高的一半， 代码展示如下：  
    ```css
    body {
        color: #ffffff;
        background: #444444;
    }
    
    .book {
        width: 300px;
        height: 300px;
        position: absolute;
        top: 50%;
        left: 50%;
        /* 第一种 */
        /* 兼容性 未使用css3, ie678 */
        /* margin-left: -150px; */
        /* margin-top: -150px; */
        /*第二种*/
        -webkit-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);

    }
    ```  
    
    两种方法第一种的兼容性更加的好一些，因为其中没有使用Css3的属性 对于ie678的兼容比较友好

