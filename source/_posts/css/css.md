---
title: CSS背景图片处理
category: css
tags: [css,背景图片]
---
前端设计页面时，经常会遇到背景图片处理的问题，我们来介绍一下常见的几种背景图片的处理方法：
#### 背景透明度问题
 1 背景透明
 ```
 background-color:transparent;背景透明
 ```
 2 背景颜色透明
 ```
 background: rgba(255,127,80,0.3);// RGBA（红、绿、蓝、透明度）
 background: hsla(0,100%,50%,0.5);// HSLA（色调、饱和、亮度、透明度）
 ```
 3 单独设置透明度
 ```
 opacity:0.7;//透明度
 ```
 #### 背景样式处理
 背景平铺
```
 background-image: url(../img/homepage.jpg);//图片
 background-repeat: no-repeat;  //不可重复
 background-clip: border-box;  //不可以在边框中显示
 background-color: #F4BF31; //颜色
 background-size: cover;//铺满
```
