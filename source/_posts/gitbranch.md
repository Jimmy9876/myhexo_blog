---
title: git养成记之一
date: 2017-05-25 16:56:45
tags: git
copyright: true
---

> 今天，简单了解了一下关于git分支的用法

场景：由于项目需要，我们团队进行开发，各个成员完成各自的功能模块，但是在git上上传的时候非常乱，这个时候，我们需要用到分支branch，当然这个功能只是分支的一部分功能，还有很多功能后续我会再进行深度学习了解。



## 1.首先

找到团队的GitHub地址，把他克隆下来

```shell
git clone https://xxxxxx.xxxx/xxxx(你的项目地址)
```

克隆完成之后，cd进入你的项目

```shell
cd 你的项目名称
```
然后，你开始开发你的功能了

## 2.新建一个分支

接下来，我们新建一个分支

```shell
git branch <your branch name>(你的分支名)
```

然后，切换一下分支

```shell
git checkout <your branch name>(你的分支名)
```

切换成功terminal输出如下

```shell
Switched to branch <your branch name>(你的分支名)
```

我们`git status`一下，看一下改动的文件，红色的是你修改过的文件，

然后执行`git add -f`，这时你再`git status`一下，是不是发现红色的文件都变成绿色了。

然后运行

```shell
git commit -m "你的注释/可以写写改了啥功能，或者就是什么版本啊balabala"
```

`commit`成功了控制台大概如下输出

```powershell
[experiment e465517] branch
 1 file changed, 1 insertion(+)
 create mode 100644 hello/hello
```

最后，运行一下代码把你项目提交上去

```
git push origin <your branch name>(你的分支名)
```

成功了大概terminal显示如下

```shell
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 311 bytes | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
To https://git.coding.net/CodeTiger_/livec_news.git
 * [new branch]      experiment -> experiment
```

至此，就全部完成了，如有疑问或者文章存在任何错误，欢迎指正😆370555337@qq.com