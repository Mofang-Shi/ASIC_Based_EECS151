# `git`&`gh`教程

教程来自：[史上最浅显易懂的Git教程！](https://www.liaoxuefeng.com/wiki/896043488029600)


## 一、`Git`和Github CLI（`gh`）之间的区别


**Git**

`Git`是一个开源的分布式版本控制系统，最初由林纳斯·托瓦兹（Linus Torvalds）于2005年创建。

它被广泛用于软件开发中，以管理项目的更改历史记录和版本控制。`Git`允许多个开发者在同一项目上独立地工作，并可以轻松地合并和管理代码。

`Git`的核心理念是每个开发者都有一个完整的本地存储库，使他们能够在离线状态下进行工作。这些本地存储库可以与其他开发者的存储库同步，以便更好地协同工作。Git通过使用分支和合并的概念，使多人协作开发变得更加高效。

**Github CLI**

Github CLI（简称`gh`）是Github官方提供的命令行接口，用于与Github进行交互。它提供了一系列命令，允许用户在命令行中管理存储库、问题、拉取请求等Github上的内容。

通过Github CLI，用户可以通过简单的命令来完成常见的Github操作，例如创建和克隆存储库、提交和推送更改、创建问题和拉取请求等等。Github CLI提供了一种更快捷和便利的方式来与Github进行交互，尤其适用于喜欢在命令行中工作的开发者。

## 二、Git基本操作

### 1.创建本地库

首先，新建一个库要存放内容的文件夹，并进入文件夹：

```shell
shimofang@shimofang-virtual-machine:~$ mkdir ./my_first_repo
shimofang@shimofang-virtual-machine:~$ cd ./my_first_repo
```

然后，通过`git init`命令把这个目录变成`Git`可以管理的仓库：

```shell
shimofang@shimofang-virtual-machine:~/my_first_repo$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /home/shimofang/my_first_repo/.git/

```


### 2.添加文件

把文件添加到版本库一定要确保文件放到了库的目录下（或者子目录）：

``` shell
shimofang@shimofang-virtual-machine:~/my_first_repo$ git add list.txt
shimofang@shimofang-virtual-machine:~/my_first_repo$ git add list_sorted.txt
```

然后用命令`git commit`告诉`Git`，把文件提交到了仓库：

```shell
shimofang@shimofang-virtual-machine:~/my_first_repo$ git commit -m 'my first add'
[master (root-commit) 1ccc033] my first add
 2 files changed, 21 insertions(+)
 create mode 100755 list.txt
 create mode 100644 list_sorted.txt
```

### 3.修改文件

简单修改一下`list.txt`，`git status`命令可以让我们时刻掌握仓库当前的状态：

```shell
shimofang@shimofang-virtual-machine:~/my_first_repo$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   list.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

上面的命令输出告诉我们，`list.txt`被修改过了，但还没有准备提交的修改。虽然`Git`告诉我们`list.txt`被修改了。

如果要看具体修改了什么内容，需要用`git diff`这个命令看看：

```shell
shimofang@shimofang-virtual-machine:~/my_first_repo$ git diff list.txt
diff --git a/list.txt b/list.txt
index d5f07f9..7968da7 100755
--- a/list.txt
+++ b/list.txt
@@ -2,10 +2,11 @@
 桌面
 Doc
 Downloads
-L1Q5
+L5Q1
 Music
 Picture
 Public
 snap
 Video
 666666
+new line

```

知道了对`list.txt`作了什么修改后，再把它提交到仓库就放心多了。

提交修改和提交新文件是一样的两步，第一步是`git add`，然后可以`git status`查看状态，最后`git commit -m "message"`。

