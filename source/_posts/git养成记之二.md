---
title: git养成记之二
copyright: true
date: 2017-05-27 13:03:09
tags: git
---

> 前几天发现，`-f`是`force`强推，即利用强覆盖方式用你本地的代码替代git仓库内的内容，所以说`git push -f`是一个比较可怕的命令，和`rm -rf`一样可怕😨 

### 但是如果你不强推，可能就出现了这样的错误

`error:failed to push some refs to …`

当要push代码到git时，出现提示：

```Shell
error:failed to push some refs to ...

Dealing with “non-fast-forward” errors

From time to time you may encounter this error while pushing:

$ git push origin master 

To ../remote/ 

 ! [rejected]        master -> master (non-fast forward) 

error: failed to push some refs to '../remote/' 

To prevent you from losing history, non-fast-forward updates were rejected

Merge the remote changes before pushing again.  See the 'non-fast forward'

section of 'git push --help' for details.
```

问题（Non-fast-forward）的出现原因在于：git仓库中已经有一部分代码，所以它不允许你直接把你的代码覆盖上去。

强推是解决办法之一，不过强推会覆盖之前的东西。。。至于覆盖了能不能找回，我还没有具体研究。

另外还有一个办法，先把git的东西fetch到你本地然后merge后再push。

```Shell
git fetch
git merge
```

这2句命令等价于

```Shell
git pull	
```

可是，这时候又出现了如下的问题：

上面出现的 [branch "master"]是需要明确(.git/config)如下的内容

```shell

[branch "master"]

    remote = origin

    merge = refs/heads/master
```

这等于告诉git2件事:

1，当你处于`master branch`, 默认的`remote`就是`origin`。

2，当你在`master branch`上使用`git pull`时，没有指定`remote`和`branch`，那么`git`就会采用默认的`remote`（也就是`origin`）来`merge`在`master branch`上所有的改变

如果不想或者不会编辑`config`文件的话，可以输入如下命令行：

```Shell
$ git config branch.master.remote origin 

$ git config branch.master.merge refs/heads/master 
```

之后再重新`git pull`下。最后`git push`你的代码吧。

总结：你的本地代码和远程仓库有冲突的时候，就会提示以上错误，说白了你就是要解决这些冲突，这样才能`push`到远程仓库当中去。如有疑问，欢迎留言交流。