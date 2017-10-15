---
title: 让你的hexo博客支持LaTex数学公式
copyright: true
date: 2017-06-11 16:21:20
mathjax: true
tags: hexo
---

## 利用MathJax来渲染LaTeX数学公式

<!--more-->

经过一番google之后，发现有位高手已经写好了一个自动部署MathJax的hexo插件 
[http://catx.me/2014/03/09/hexo-mathjax-plugin/](http://catx.me/2014/03/09/hexo-mathjax-plugin/) 
安装方式也很简单，在你的博客文件夹下执行

```shell
npm install hexo-math --save
hexo math install
```

**这里npm如果缓慢，请自行换成淘宝镜像源**

**关于淘宝镜像源，在之前文章中有提到，请自行查阅**

然后在新建的博文中写上一个查看LaTeX效果

```latex
\begin{align}
\theta\_0 & := \theta\_0 - \alpha\frac{\partial}{\partial\theta\_0}J(\theta\_0,\theta\_1) \\\\
& = \theta\_0 - \alpha\frac{\partial}{\partial\theta\_0} \frac{1}{2m} \sum\_{i=1}^{m}(h\_\theta(x^{(i)}) - y^{(i)})^2 \\\\
& = \theta\_0 - (\alpha \frac{1}{2m} \* 2 \* \sum\_{i=1}^{m}(h\_\theta(x^{(i)}) - y^{(i)})) \* \frac{\partial}{\partial\theta\_0}(h\_\theta(x^{(i)}) - y^{(i)}) \\\\
& = \theta\_0 - \frac{\alpha}{m}  * \sum\_{i=1}^{m}(h\_\theta(x^{(i)}) - y^{(i)})
\end{align}
```

$$
R_{m \times n} = U_{m \times m} S_{m \times n} V_{n \times n}'
$$

嗯，发现一切显示完美...