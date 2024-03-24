---
title: "test_post_git"
date: 2021-09-15T22:22:11+08:00
tags: ["git","github"]
toc: true
---


## 基本操作

### 配置用户名和地址

```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
$ git config -l //查看当前配置
```
注意`git config`命令的`--global`参数，用了这个参数，表示这台机器上所有的Git仓库都会使用这个配置。也可以对某个仓库指定不同的用户名和Email地址。

---

### 初始化一个git仓库

使用` git init` 命令

### 添加文件到git仓库

#### step1

用命令`git add <file>`，可反复多次使用，添加多个文件

**1、添加所有文件**到暂存区

一般情况下，我们会用 `.` 或者 `*` 来提交，表示的是所有，是一种正则表达式。

不加参数默认为将修改操作的文件和未跟踪新添加的文件添加到git系统的暂存区，注意不包括删除。

```shell
git add *
```

```shell
git add .
```

**拓展：**

```shell
git add -u .
```

-u 表示将已跟踪文件中的修改和删除的文件添加到暂存区，不包括新增加的文件，注意这些被删除的文件被加入到暂存区再被提交并推送到服务器的版本库之后这个文件就会从git系统中消失了。

```shell
git add -A .
```

-A 表示将所有的已跟踪的文件的修改与删除和新增的未跟踪的文件都添加到暂存区。

**2、添加某个文件类型**到暂存区，比如所有的 `.html` 文件。

```shell
git add *.html
```

**3、添加整个文件夹**到暂存区，比如根目录的 index 文件夹。

```zsh
git add index/
```

**4、添加某个文件或者某个文件夹中的某个文件**到暂存区 ，比如 index 下的 `index.html` 文件。

```zsh
git add index/index.html
```

#### step2

使用命令`git commit -m <message>`，完成

## 仓库版本管理


### 掌握仓库当前的状态

命令`git status`

### 查看内容的修改部分

命令`git diff`

### 显示从最近到最远的修改日志

命令`git log`

可以使用--pretty=oneline参数 如` git log --pretty=oneline `减少输出的信息

### 版本回退

#### 把文件回退到之前的版本

在Git中，用`HEAD`表示当前版本,上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，往上100个版本写成`HEAD~100`。

回退版本使用`git reset`命令 如`$ git reset --hard HEAD^  `  (--hard 是参数)

#### 恢复到回退前的版本

```shell
$ git reset --commit id (few numbers are ok)
```

  <mark>可以通过查看命令历史的命令`git reflog` 来查看之前版本的版本号</mark>

### 撤销对文件的修改

#### 工作区的撤销

`git checkout -- <file>`可以丢弃工作区的修改

<mark>命令`git checkout -- <file>`意思是，把文件在工作区的修改全部撤销</mark>，这里有两种情况：

- 一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

- 一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

<mark>总之，就是让文件回到最近一次`git commit`或`git add`时的状态。</mark>

#### 暂存区的撤销

用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区

### 从版本库中删除文件


#### 删除

从版本库中删除文件，用命令`git rm`删掉，并且`git commit`

```shell
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
```

 <mark>提示：先手动删除文件，然后使用`git rm  \<file\`和`git add\<file\>`效果是一样的。</mark>

#### 恢复

如果删错了，因为版本库里有，所以可以把误删的文件恢复到最新版本：

```shell
$ git checkout -- test.txt
```

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

 <mark>注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！</mark> 

## 远程仓库

### 添加远程库

#### step1

现在，我们根据GitHub的提示，在本地的仓库下运行命令：

```shell
$ git remote add origin git@github.com:username/repo.git
```

#### step2

把本地库的所有内容推送到远程库上：

```shell
$ git push -u origin main
```

`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送到远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

从现在起，只要本地作了提交，就可以通过命令：

```shell
$ git push origin master
```

把本地`master`分支的最新修改推送至GitHub

### 修改远程库

```shell
git remote set-url origin <url>
```

### 删除远程库

如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。<mark>使用命令`git remote -v`可以查看远程库信息</mark>

然后，根据名字删除，比如删除`origin`：

```shell
$ git remote rm origin
```

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

### 从远程库克隆

上面是先有本地库，后有远程库时，关联远程库的方法。

而从零开发最好的方式是先创建远程库，然后从远程库克隆

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

Git支持多种协议，包括`https`，而`ssh`协议速度最快。

