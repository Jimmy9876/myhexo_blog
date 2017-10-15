---
title: Hexo+Next主题个性化配置-1
copyright: true
date: 2017-05-30 10:53:55
tags: hexo
---

> 折腾了next这么久，就写一篇博客来记录一下，以作备忘，同时也给后来人一些借鉴



<!--more-->


# NexT主题安装使用

## 本地环境

自行安装 `git` 和 `Node.js` 不会的可百度，安装方法一堆。

## 安装Hexo

`Git` 和 `Node.js` 都安装好后,首先创建一个用于存放博客文件的文件夹，如 `blog`，然后进入 `blog` 文件夹，下面开始安装并使用 `Hexo`。
右键选择 `Git Bash Here`，弹出 `Git Bash` 窗口；执行命令：

```
$ npm install -g hexo-cli
$ hexo init

```

安装完成后，指定文件夹的目录如下：

```
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

```

其中 `_config.yml` 文件用于存放网站的配置信息，你可以在此配置大部分的参数； `scaffolds` 是存放模板的文件夹，当新建文章时，Hexo 会根据 `scaffold` 来建立文件； `source` 是资源文件夹，用于存放用户资源， `themes`是主题文件夹，存放博客主题， `Hexo` 会根据主题来生成静态页面。

在 `Git Bash` 终端执行命令：

```
$ hexo g
$ hexo s

```

Hexo将 `source` 文件夹中的Markdown 和 HTML 文件会被解析并放到 `public` 文件夹中， `public` 文件夹用于存放静态博客文件，相当于网站根目录。
至此博客雏形基本完成，在浏览器中访问 `http://localhost:4000/` ，就可以访问本地博客了。

## 使用NexT主题

在 `Git Bash` 终端执行以下命令：

```
$ git clone https://github.com/iissnan/hexo-theme-next themes/next

```

打开站点配置文件 `_config.yml`，找到 `theme` 字段，并将其值更改为 `next` 。

```
theme: next

```

NexT主题是我用过的唯一的一款Hexo主题，界面简约，功能齐全且多样，响应式设计，电脑，手机访问效果很好。

在 `Git Bash` 终端执行命令 `hexo s` ，在浏览器中访问 `http://localhost:4000/` ，可以看到默认的NexT-Muse主题。

我喜欢双栏的故使用 `NexT.Pisces` 主题，修改主题配置文件  `_config.yml`的 `Schemes` 字段的值为：

```
scheme: Pisces

```

# Next主题宽度调节

现在一般都用宽屏显示器，博客页面两侧留白太多，调整一下宽度。
打开 `\themes\next\source\css\_common\components\post\post-expand.styl` 文件，找到

```
@media (max-width: 767px)

```

改为

```
@media (max-width: 1080px)

```

打开 `\themes\next\source\css\ _variables\base.styl` 文件，找到

```
$main-desktop                   = 960px
$main-desktop-large             = 1200px
$content-desktop                = 700px

```

修改 `$main-desktop` 和 `$content-desktop` 的数值：

```
$main-desktop                   = 1080px
$main-desktop-large             = 1200px
$content-desktop                = 810px

```

`Next.Mist` 主题的文章宽度至此改完了。如果你用的是 `Next.Pisces`，还需要继续修改。
打开 `\themes\next\source\css\_schemes\Pisces\_layout.styl` 文件，将第 `4` 行的 `width改为1080px` ，修改后如下：

```
.header {
  position: relative;
  margin: 0 auto;
  width: 1080px;

```

记录一下我常用的细节改动，参考了许多博友的设置，并不是我的原创。参考网站，会在文章最底部列出，以示谢意。

# 修改文章内链接文本样式

将链接文本设置为蓝色，鼠标划过时文字颜色加深，并显示下划线。
修改文件 `themes\next\source\css\_common\components\post\post.styl` ，添加如下css样式，：

```
// 文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}

```

选择 `.post-body` 是为了不影响标题，选择 `p` 是为了不影响首页“阅读全文”的显示样式。

# 文章底部的那个带#号的标签

文章底部的那个带#号的标签，比如#NexT，可以把#换成图标吗，怎么设置?
修改模板 `layout/_macro/post.swig`，搜索 `rel="tag">#`，将 # 换成 `<i class="fa fa-tag"></i>`

# 首页展示文章动画效果和图片放大镜效果关闭哪改？

文章动画效果关闭：主题配置里 `Motion:` 改为 `false`

关闭图片放大镜效果: 主题配置里 `fancybox:` 改为 `false`

# hexo背景动态效果和心心

博客背景动态效果图和点击小红心效果的相关设置。
把 `js` 文件 `love.js` 和 `particle.js` 放在 `\themes\next\source\js\src` 文件目录下
更新 `\themes\next\layout\_layout.swig` 文件，在末尾（在前面引用会出现找不到的bug）添加以下 `js` 引入代码：

```
<!-- 背景动画 -->
<script type="text/javascript" src="/js/src/particle.js"></script>
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>

```

想设置动画线条颜色可改为：

```
<script type="text/javascript" color="255,0,0" opacity="0.3" count="99" src="particle.js"></script>

```

就能显示红色。或者用：

```
<script type="text/javascript" src="/js/src/particles.js" count="50" zindex="-2" opacity="1" color="0,104,183"></script>

```

两个JS下载为：

```
http://7u2ss1.com1.z0.glb.clouddn.com/love.js
http://7u2ss1.com1.z0.glb.clouddn.com/particle.js

```

# hexo NexT主题首页title的优化

更改 `index.swig` 文件，文件路径是 `your-hexo-site\themes\next\layout` ，将下面代码

```
{% block title %} {{ config.title }} {% endblock %}

```

改成

```
{% block title %} {{ config.title }} - {{ theme.description }} {% endblock %}

```

这时候你的首页标题会更符合网站名称 - 网站描述这习惯。
进阶，做了 `seo` 优化，把关键词也显示在 `Title` 标题里，可改成

```
{% block title %} {{ theme.keywords }} - {{ config.title }} - {{ theme.description }} {% endblock %}

```

**注意：**别堆砌关键字，整个标题一般不超过 `80` 个字符，可以通过chinaz的seo综合查询检查。

# 每篇文章末尾统一添加“本文结束”标记

## 新建 `passage-end-tag.swig` 文件

在路径 `\themes\next\layout\_macro` 中添加 `passage-end-tag.swig` 文件，其内容为：

```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">------本文结束<i class="fa fa-paw"></i>感谢阅读------</div>
    {% endif %}
</div>

```

## 修改 post.swig 文件

在 `\themes\next\layout\_macro\post.swig` 中， `post-body` 之后， `post-footer` 之前添加如下代码（post-footer之前两个DIV）：

```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>

```

## 在主题配置文件中添加字段

在**主题配置文件** `_config.yml` 中添加以下字段开启此功能：

```
# 文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true

```

完成以上设置之后，在每篇文章之后都会添加“本文结束”标记。

# 增加HIGH一下功能

在 `themes\next\layout\_macro` 目录下增加 `high.swig` 文件，我已改为歌曲循环和多次点击不重复！
地址为:

```
http://7u2ss1.com1.z0.glb.clouddn.com/high-xunhuan.swig

```

打开这个地址，复制全部内容，在你本地新建`high.swig` 文件。
打开\themes\next\layout\_macro\sidebar.swig文件，打开，在

```
<a href="{{ url_for(theme.rss) }}" target="_blank" rel="alternate">
    <i class="fa fa-rss"></i>
    RSS
</a>

```

后边加入：

```
{% include 'high.swig' %}

```

如：

```
{% if theme.rss %}
          <div class="feed-link motion-element">
            <a href="{{ url_for(theme.rss) }}" rel="alternate">
              <i class="fa fa-rss"></i>
              RSS
            </a>
              {% include 'high.swig' %}
          </div>
        {% endif %}

```

接着在主题配置文件 `_config.yml` ，加入：

```
highqilai: 
  enabled: true

```

然后打开自定义CSS： `\themes\next\source\css\_custom\custom.styl` 加入

```
.feed-link a{display: inline-block;}

```

保存，`hexo clean` ， `hexo g` , `hexo s` 查看效果！
主页 `High` 起来，摇动。改动方法！
`themes\next\layout\_layout.swig`
前添加：

```
<link href="http://7u2ss1.com1.z0.glb.clouddn.com/harlem-shake-style.css" rel="stylesheet" type="text/css" />

```

地址改为你自己的CSS。失效了不怪！
*如果只是想当播放器听歌的话改 high.swig 文件内容为：*

```
<a title="收藏到书签，偶尔High一下^_^" rel="alternate" class="mw-harlem_shake_slow wobble shake" href='javascript:(
    /*
     * Copyright (C) 2015 Rocko (rocko.xyz) <rocko.zxp@gmail.com>
     *
     * Licensed under the Apache License, Version 2.0 (the "License");
     * you may not use this file except in compliance with the License.
     * You may obtain a copy of the License at
     *
     *      http://www.apache.org/licenses/LICENSE-2.0
     *
     * Unless required by applicable law or agreed to in writing, software
     * distributed under the License is distributed on an "AS IS" BASIS,
     * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
     * See the License for the specific language governing permissions and
     * limitations under the License.
     */
    function go() {
    
      var songs = [
          "http://7u2ss1.com1.z0.glb.clouddn.com/%E9%AB%98%E6%A2%A8%E5%BA%B7%E6%B2%BB%20-%20%E5%AD%A4%E7%8B%AC.mp3", 
          "http://7u2ss1.com1.z0.glb.clouddn.com/one%20by%20one.mp3",
          "http://7u2ss1.com1.z0.glb.clouddn.com/Enya%20-%20Only%20Time.mp3",
          "http://7u2ss1.com1.z0.glb.clouddn.com/Enya%20-%20May%20It%20Be.mp3",        
          "......"
      ];
 
      function S() {
          var e = document.getElementById("audio_element_id");
          if(e != null){
              var index = parseInt(e.getAttribute("curSongIndex"));
              if(index > songs.length - 2) {
                  index = 0;
              } else {
                  index++;
              }
              e.setAttribute("curSongIndex", index);
          }
          e.src = i;
          e.play()
      }
      function initAudioEle() {
          var e = document.getElementById("audio_element_id");
          if(e === null){
            e = document.createElement("audio");
            e.setAttribute("curSongIndex", 0);
            e.id = "audio_element_id";
            e.loop = false;
            e.bgcolor = 0;
            e.innerHTML = " <p>If you are reading this, it is because your browser does not support the audio element. We recommend that you get a new browser.</p> <p>";
            document.body.appendChild(e);
            e.addEventListener("ended", function() {
              go();
            }, true);
          }        
      }
    
      initAudioEle();
      var curSongIndex = parseInt(document.getElementById("audio_element_id").getAttribute("curSongIndex"));
      var i = songs[curSongIndex];
      S();
    })()'>
    <i class="fa fa-music"></i> 听音乐</a>

```

# 作者头像变成圆形

打开自定义CSS： `\themes\next\source\css\_custom\custom.styl` 加入

```
.site-author-image {
  border-radius: 100%;
  padding: 2px;
  border: 2px dashed #fff;
  animation: cycle 2s 0.5s forwards;
  transition: border-radius 2s;
}

```

博主名字号大小,也在 `custom.styl` 文件:

```
.site-author-name {
  font-size: 16px;
}

```

# 动态title改动

先看代码如下：

```
<!--崩溃欺骗-->
var OriginTitile = document.title;
 var titleTime;
 document.addEventListener('visibilitychange', function () {
     if (document.hidden) {
         $('[rel="icon"]').attr('href', "/img/TEP.ico");
         document.title = '╭(°A°`)╮ 页面崩溃';
         clearTimeout(titleTime);
     }
     else {
         $('[rel="icon"]').attr('href', "/favicon.ico");
         document.title = '(ฅ>ω<*ฅ) 噫又好了~' + OriginTitile;
         titleTime = setTimeout(function () {
             document.title = OriginTitile;
         }, 2000);
     }
 });

```

做为JS引用时，可以直接将上面代码保存为XXX.js，然后引用。在 `\themes\next\layout\_layout.swig` 最下边引用加入：

```
<!--崩溃欺骗-->
<script type="text/javascript" src="/js/src/duoshuoshuo.js"></script>

```

# hexo站点添加sitemap网站地图

## 安装hexo的sitemap网站地图生成插件

进入 `hexo` 根目录，打开 `git`

```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save

```

## 在你的hexo站点的_config.yml添加下面的代码，注意缩进格式！

```
# hexo sitemap网站地图
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml

```

### 配置成功后

hexo编译时会在hexo站点根目录生成sitemap.xml和baidusitemap.xml
其中sitemap.xml适合提交给谷歌搜素引擎，baidusitemap.xml适合提交百度搜索引擎。
其次，在robots.txt中添加下面的一段代码：

```
Sitemap: http://你的域名/sitemap.xml
Sitemap: http://你的域名/baidusitemap.xml

```

请自行改成自己的网站。


# 给 Github 添加 README

默认情况下， `Github` 中每一个项目，我们希望有一份 `README.md` 的文件来作为项目的说明，但是我们在项目根目录下的 `blog\source` 目录下创建一份 `README.md` 文件，写好说明介绍，部署的时候，这个 `README.md` 会被 `hexo` 解析掉，而不会被解析到 `Github` 中去的。
正确的解决方法其实很简单：
把 `README.md` 文件的后缀名改成 `MDOWN` 然后扔到 `blog/source` 文件夹下即可，这样 `hexo` 不会解析， `Github` 也会将其作为MD文件解析。

# 代码块自定义样式``内的

打开自定义CSS： `\themes\next\source\css\_custom\custom.styl` 加入

```
// 代码块自定义样式``内的
code {
    color: #fc6423;
    background: #fbf7f8;
    margin: 2px;
}
// 大代码块的自定义样式
.highlight, pre {
    margin: 5px 0;
    padding: 5px;
    border-radius: 3px;
}
.highlight, code, pre {
    border: 1px solid #d6d6d6;
}

```

# 博客部署的message

`\node_modules\hexo-deployer-git\lib\deployer.js` 文件末尾找到这一句：

```
Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}.

```

改得个性化一点：

```
这个勤奋的家伙又更新了: {{ now(\'YYYY-MM-DD HH:mm:ss\') }}.

```

# 博文置顶

## 修改 `hexo-generator-index` 插件

替换文件：`node_modules/hexo-generator-index/lib/generator.js`为：

```
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};

```

## 设置文章置顶

在文章 `Front-matter` 中添加 `top` 值，数值越大文章越靠前，如：

```
---
title: Hexo
date: 
tags: 
categories: 
top: 10
---

```

# NexT主题自定义无序列表样式

打开自定义CSS： `\themes\next\source\css\_custom\custom.styl` 加入：

```
ul {
list-style-type: circle;  // 空心圆，实心圆为 disc
}
```
[原文链接](http://jimmy9876.top)

部分内容来自以下博客：
[务虚笔记](http://www.wuxubj.cn/)
[小桥流水人家](http://ehlxr.me/)
[Jing’s Blog](http://www.iamlj.com/)
[Doublemine](https://notes.wanghao.work/)
[岁月如歌](http://lovenight.github.io/)
[胡闹的日子](http://hunao.info/)
[Never_yu’s Blog ](https://neveryu.github.io/)
