---
title: Git&Github 学习笔记
date: 2017-10-03 12:46:39
tags:
  - Git
  - Github
  - 学习
categories:
  - Git&GitHub
---
<center>Git&GitHub学习笔记</center>

<!-- more -->

## 1.1 省略
## 1.2
本地 & 与他人合作

> 创建github账号
>
> 安装git

## 1.3
config:
```
user.name and user.email
git config --global color.ui auto
```
local > global > system

## 1.4 init
初始化 (本地)

```
已存在的项目进行版本控制
ls -l
git init
git status
```
or
```
创建新项目
git init '项目名称'
```
初始(云端)
> Create a new repository

## 1.5 Commit
> **对改动进行提交**

三种方法：
> 1.命令行提交
> ```
> 相关命令(待实际测试)
> ls -la
> git status
> vi '文件名' (使用文本编辑器进行编辑)
> git add '文件名' (放入 *暂存区*)
> git commit -m '描述信息'
> ```
> 2.Github.Com
>
> 3.Github客户端

## 1.6 Diff
> **查询所做的修改**

相关命令：
> ```
> git diff
> # 查询未存档文件(工作树)的改动
> ```
> ```
> git diff --staged
> # 暂存区 与 已提交历史文件 的区别
> ```
> ```
> git diff HEAD
> # 工作树与最近一次提交相比较
> ```
> ```
> git diff --color-words
> git diff --word-diff
> git diff --stat
> # 标出修改位置/输出修改情况
> ```

## 1.7 Log
> **查询更新日志**

相关命令：
> ```
> git log
> # 提交日志
> git log --oneline
> # 更新的简短概要(更新历程)
> git log --stat
> # 每次提交包含的文件及其改动
> git log --patch
> # 每次commit之间的改动(+/-,G/R)
> git log --graph
> # 图形化展示分支合并历史
> ```

以上命令可以组合使用，例如：
> git log --graph --all --oneline

## 1.8 Remove
> **清理冗余数据**

相关命令:
> ```
> git rm file
> # 删除文件 并在status中暂存删除状态
> ```
> ```
> git add -u .
> # 遍历工作目录，暂存可被删除文件的状态
> ```
> ```
> git rm --cached
> # 处理误提交文件
> ```

另外，也可**直接删除**文件，然后通过**桌面客户端**保存修改。

## 1.9 Move
> **移动文件**

相关命令:
> ```
> git mv 旧地址 新地址
> # 如未使用git指令进行mv，需要先rm，再add。
> ```
> ```
> git add -A .
> # 发现当前目录所有新文件，并暂存保存状态
> ```
> ```
> git log --stat -- filename
> # 展示该文件的全部提交
> git log -M --follow
> # 添加参数，跟踪文件移动前的改动历史
> ```
> 相似度(默认50%)：如果超过阈值，则git会在移动中跟踪它，认为它是一个移动而不仅仅是一个删除和添加。

## 1.10 Ship of Theseus
关于版本控制的哲学问题。

CVS/企业/git

版本控制系统之间的差异。

## 1.11 Ignore
> **避免提交某些文件**

相关命令：
> ```
> # 创建 .gitignore 文件
> touch .gitignore
> git add .gitignore
> git commit -m'描述信息'
> ```
> ```
># 在 .gitignore 文件中添加忽略路径/名称
> 例如：
> .sass-chche
> *.log
> tmp/
> ```
> ```
> # 查询哪些文件被忽略了
> git ls-files --others --ignores --exclude -standard
> ```

## 1.12 Branch
> **关于分支**

相关命令：
> ```
> # 创建
> git branch name
> # 删除
> git branch -d neme
> # 切换分支
> git checkout name
> ```

## 1.13 Checkout
> **切换分支及其他功能**

相关命令：
> `git checkout name` 切换分支
> ```
> # 查看更详细的commit
> git checkout '提交引用'
> # 删除该文件最近一次commit内容
> git checkout --filename
> # 创建并切换到新分支
> git checkout -b name
> ```

## 1.14 Merge
> **汇聚多个分支，合并commit**

相关命令：
> ```
> # 将某支与当前分支合并
> git merge '有commit的branch'
> ```
> ```
> # 处理merge过程中的冲突
> 打开提示的冲突文件，然后查看由>>> === <<< 分隔表示出的冲突部分，手动解决冲突。
> 处理完毕后，使用 git add 添加到暂存区，再运行 git commit结束这一过程。
> ```
> ```
> # 暂时不处理冲突(清空工作目录和暂存区)
> git merge --abort
> ```
> ```
> # 汇聚某一分支所有commit
> git merge --squash '目标分支'
> ```
> ```
> # 完成合并后，删除分支
> git branch -d '分支name'
> ```

## 1.15 Network
> **网络相关操作**

相关命令：

> ```
> # 创建remote
> git remote add 目标名称 完整url
> # 修改remote信息
> git remote set-url 目标名称 完整url
> # 移除remote
> git remote rm 目标名称
> # 查询remote信息
> git remote -v
> ```
> ```
> git fetch 目标名称
> # fetch操作
> # 在GitHub.com上抓取信息，放在remote分支里。
> ```
> ```
> git pull 目标名称
> # pull操作
> # 将GitHub.com的更新拉去到本地，然后合并。
> ```
> ```
> git push 目标名称
> # push操作
> # 将本地项目推送到GitHub
> ```

## 1.16 GUI
> **图形化用户界面**

## 1.17 GitHub介绍
> **GitHub相关特点的一些介绍**

## 1.18 Forking
> **将项目拷贝到仓库中，可安全的进行修改**

## 1.19 Pull Requests
> **提交修改到其他代码库**
>
> **开始编辑 让它更好**

## 1.20 Reset
> **对历史commit的操作方式**

相关命令：
> git reset --mixed、soft、hard

## 1.21 Reflog
> **追踪对修改内容的修改**

相关命令：
> ```
> git reflog
> # 可查看修改历史，并可通过哈希串恢复回历史节点。
> git reset --hard 哈希串
> # 切换回历史节点
> ```
> 通过频繁提交，可保证代码安全，可随时进行恢复。

## 1.22 Rebase
> **将分支进行重定位**
> 待实际操作



## 结束
看着官方视频，整理了一下常用的操作命令。


视频点这里：
[GitHub&Git入门基础](https://www.nowcoder.com/courses/2#chapter-14)
