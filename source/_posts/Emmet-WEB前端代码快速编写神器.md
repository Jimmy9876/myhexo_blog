---
title: Emmet:WEB前端代码快速编写神器
copyright: true
date: 2017-06-07 13:30:09
tags: Sublime插件
---

Emmet的前身是大名鼎鼎的Zen coding，如果你从事Web[前端开发](http://lib.csdn.net/base/javascript)的话，对该插件一定不会陌生。它使用仿CSS选择器的语法来生成代码，大大提高了HTML/CSS代码编写的速度，当然Sublime Text也支持改插件，**默认在Sublime Text3种自带了这个插件**。

<!--more-->

下载Sublime Text3：[http://download.csdn.net/detail/u011127019/9596257](http://download.csdn.net/detail/u011127019/9596257)

#  一、快速格式化Html代码，输入内容然后按Tab键（注意在输入内容的结尾处）

## 1.初始化，比如输入“!”或“html:5”，然后按Tab键

![img](http://img.blog.csdn.net/20160820203739582?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

输入标签，然后Tab键

`div`

```Css
<div></div>  
```

## 2.轻松添加类、id、文本和属性

比如输入：`div#person.top`

自动生成：

```Css
<div id="person" class="top"></div>  
```

比如输入：`h1{标题}`

自动生成：

`<h1>标题</h1>  `

比如输入：`a[href=#]`

`<a href="#"></a>  `

## 3.嵌套

现在你只需要1行代码就可以实现标签的嵌套。 

- \>：子元素符号，表示嵌套的元素
- +：同级标签符号
- ^：可以使该符号前的标签提升一行

效果如下图所示： 

![img](http://img.blog.csdn.net/20160820205826673?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## 4.分组

你可以通过嵌套和括号来快速生成一些代码块，比如输入`(.foo>h1)+(.bar>h2)`，会自动生成如下代码： 

```Css
<div class="foo">  

  <h1></h1>  

</div>  

<div class="bar">  

  <h2></h2>  

</div>  

```



## 5.隐式标签

声明一个带类的标签，只需输入div.item，就会生成`<div class="item"></div>`。 
在过去版本中，可以省略掉div，即输入.item即可生成`<div class="item"></div>`。现在如果只输入.item，则Emmet会根据父标签进行判定。比如在`<ul>`中输入.item，就会生成`<li class="item"></li>`。 
下面是所有的隐式标签名称： 

- li：用于ul和ol中

- tr：用于table、tbody、thead和tfoot中

- td：用于tr中

- option：用于select和optgroup中

## 6.定义多个元素 

要定义多个元素，可以使用*符号。比如，ul>li*3可以生成如下代码：

```Css
<ul>  

  <li></li>  

  <li></li>  

  <li></li>  

</ul>  

```



## 7.定义多个带属性的元素

 

如果输入 ul>li.item$*3，将会生成如下代码： 

```css
<ul>  

  <li class="item1"></li>  

  <li class="item2"></li>  

  <li class="item3"></li>  

</ul>  
```



更多请参考：[http://www.iteye.com/news/27580](http://www.iteye.com/news/27580)

文档：[http://docs.emmet.io/](http://docs.emmet.io/)（其中包含了一个Demo，你可以试验文中所提到的这些缩写） 

Via [smashingmagazine](http://coding.smashingmagazine.com/2013/03/26/goodbye-zen-coding-hello-emmet/)

更多技术干货—[Jimmy的技术乐园](http://jimmy9876.top)