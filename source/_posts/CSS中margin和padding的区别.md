---
title: CSS中margin和padding的区别
copyright: true
date: 2017-06-03 16:56:57
tags: css
---

> padding margin都是边距的含义，关键问题得明白是什么相对什么的边距．padding是控件的内容相对控件的边缘的边距．margin是控件边缘相对父空间的边距．



<!--more-->

在CSS中margin是指从自身边框到另一个容器边框之间的距离，就是容器外距离。在CSS中padding是指自身边框到自身内部另一个容器边框之间的距离，就是容器内距离。

 

**下面是 padding和margin常用的用法**

 

**一、padding**

 

**1、语法结构**

（1）padding-left:10px; 左内边距

（2）padding-right:10px; 右内边距

（3）padding-top:10px; 上内边距

（4）padding-bottom:10px; 下内边距

（5）padding：10px; 四边统一内边距

（6）padding:10px 20px; 上下、左右内边距

（7）padding:10px 20px 30px; 上、左右、下内边距

（8）padding:10px 20px 30px 40px; 上、右、下、左内边距

 

**2、可能取的值**

（1）length  规定具体单位记的内边距长度

（2）%       基于父元素的宽度的内边距的长度

（3）auto    浏览器计算内边距

（4）inherit 规定应该从父元素继承内边距

 

**3、浏览器兼容问题**

（1）所有浏览器都支持padding属性

（2）任何版本IE都不支持属性值“inherit”

 

 

**二、margin**

 

**1、语法结构**

（1）margin-left:10px; 左外边距

（2）margin-right:10px; 右外边距

（3）margin-top:10px; 上外边距

（4）margin-bottom:10px; 下外边距

（5）margin:10px; 四边统一外边距

（6）margin:10px 20px; 上下、左右外边距

（7）margin:10px 20px 30px; 上、左右、下外边距

（8）margin:10px 20px 30px 40px; 上、右、下、左外边距

 

**2、可能取的值**

（1）length  规定具体单位记的外边距长度

（2）%       基于父元素的宽度的外边距的长度

（3）auto    浏览器计算外边距

（4）inherit 规定应该从父元素继承外边距

 

**3、浏览器兼容问题**

（1）所有浏览器都支持margin属性

（2）任何版本IE都不支持属性值“inherit”

 

 

**三、margin和padding的区别用图表示为**

![](https://ws3.sinaimg.cn/large/006tNc79gy1fg84bkuy2tj30d1097gmd.jpg)

