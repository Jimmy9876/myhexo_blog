---
title: hexo+next搭建博客相册教程
copyright: true
date: 2017-05-26 14:59:14
tags: hexo_blog
---



1.在git上输入` hexo new page “photos”`,创建`photos`页面，之后在sourse文件夹下能够找到`photos`文件夹，在`index.md`里添加`type: photos`.
2.进入`theme`里的`next`下的`config`,在`menu`菜单下添加上`photos`页。
3.如果语言选择是`zh-hans`的话，记得在l`anguanges`里把`photos`添加进去，以确保网页显示的菜单为`photos`.
4.下面是重点，所有新建页面都可以照葫芦画瓢，`next`主题的整个网页布局都存在`layout`文件夹下，可以找到`layout`文件夹下有`layout.swig`和page.swig两个文件，`layout.swig`写的是整个页面的整体布局，`page.swig`是针对不同页面的布局。如果我们想搭建相册页，可以把自己写的相册页的代码放到`page.swig`,`page.swig`文件里div为post里有队不同页面的不同布局有分类，我们可以
```javascript
{% if page.type === “photos” %}
```
,将相册页的代码显示在这里面，用到的js和css别忘了引用，存的时候用绝对路径就可以了。还有一种方法就是把代码直接放到photos文件夹下的`index.md`里，但是这个方法的js和css布局容易出问题，两种方法，相册页存储的div不同，容易引起页面混乱。