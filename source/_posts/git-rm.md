---
title: git-rm
date: 2017-12-19 14:16:53
tags: git
---
在 <code>git</code> 使用中有时会遇到这样一中情况：

有一个 <code>aa.txt</code> 的文件希望被 <code>gitignore</code>，但是却不小心提交了，提交之后我在 <code>.gitignore</code> 文件添加了 <code>aa.txt</code> 文件的路径，当我再一次修改 <code>aa.txt</code> 文件时，<code>git status</code> 会提示 <code>aa.txt</code> 文件 <code>modified</code>，这时执行以下代码：

``` bash
$ git rm <aa.txt文件路径>
```

然后 <code>git commit</code> 即可，<code>aa.txt</code> 再被修改就不会被 git 记录了。