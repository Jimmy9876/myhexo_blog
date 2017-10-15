---
title: 正方自动测评javascript脚本
copyright: true
date: 2017-05-26 15:13:01
tags: javascript
---
>又是一年期末季，除了麻烦的期末考试还有没用的教学评价。教学评价太麻烦，就搞了个脚本来节省工作。

这是直接打最高分给老师的，除了一个较好，其他都是好。如果你需要给差评，点完脚本后自己改一下。

脚本是是用js写的，拖动下边的链接到书签栏就行了，或者直接添加书签。点击一次可以给一个老师完成评价，所有评价结束以后自己提交。

拖动我：<a href="javascript:(function(){var obj=$('iframeautoheight').contentDocument.getElementsByTagName('select'); for(i=1;i<obj.length;i++){obj[i].value='完全认同'; } var rid=Math.max(1, Math.floor(Math.random()*obj.length)); obj[rid].value='相对认同'; $('iframeautoheight').contentDocument.getElementById('Button1').click();})()" class="button button-small button-orange" onclick="alert('把我拖动到书签栏评测的时候点我就可以了');return false;">教学评价助手</a>
   拖动我：<a href="javascript:(function(){var obj=$('iframeautoheight').contentDocument.getElementsByTagName('select'); for(i=1;i<obj.length;i++){obj[i].value='好'; } var rid=Math.max(1, Math.floor(Math.random()*obj.length)); obj[rid].value='较好'; $('iframeautoheight').contentDocument.getElementById('Button1').click();})()" class="button button-small button-orange" onclick="alert('把我拖动到书签栏评测的时候点我就可以了');return false;">教师评价助手</a>

截图：
![Markdown](http://i1.piimg.com/1949/f33d22ed8a39beb1.png)
![Markdown](http://i1.piimg.com/1949/6df5a037ba269ac4.png)
其他学校要用只要修改一下赋值就行。自己查看一下网页元素，然后看一下你们学校的赋值是什么？好? 良好？自己再改一下书签就行了。