# UCB EECS151 SP22 Mofang's ASIC Lab

<p align="center">
Shi Mofang
</p>
<p align="center">
20202867@cqu.edu.cn
</p>
<p align="center">
Chongqing University
</p>

## Overview

作为一名即将转行进入微电子领域的研0学生，有必要在大四认真学习一下领域的相关基本知识。机缘巧合了解到UCB的EECS151课程，甚合我的口味，于是决定学习一下，争取达到本硕衔接的效果。

**在进行每一个实验之前，请务必向下先行阅读相应实验的准备工作！**

## 实验一：浏览计算机环境（Lab1:Getting Around the Compute Environment）

### 1、Linux环境搭建

设备型号：`MacBook Pro, 13-inch, 2019, Two Thunderbolt 3 ports`

虚拟机软件：[VMware Fusion](https://www.vmware.com/products/fusion.html)

Linux系统：[Ubuntu(来自清华镜像)](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/)

### 2、Linux基础

教程来自（英文）：[Learning the Shell](http://linuxcommand.org/lc3_learning_the_shell.php)

我的学习笔记&翻译：[Linux基础](asic_lab_1/Linux_Basic.md)

### 3、正则表达式基础

教程来自（英文）：[Learn Regular Expressions with simple, interactive exercises.](https://regexone.com)

我的学习笔记：[正则表达式基础](asic_lab_1/regular_expressions.md)

### 4、Vim编辑器基础

教程来自（英文）：[Interactive Vim tutorial](https://www.openvim.com/tutorial.html)

我的学习笔记：[Vim编辑器基础](asic_lab_1/Vim_editor_basics.md)

### 5、 `GNU Make`&Makefile基础（可选）

#### 安装

以`sudo`权限用户身份运行下面的命令：

```
sudo apt install make
```

运行下面的命令，打印 `make` 版本，验证安装过程：

```
make --version
```

#### Makefile基础（可选）

教程来自（英文）：[A Simple Makefile Tutorial](https://cs.colby.edu/maxwell/courses/tutorials/maketutor/)

我的学习笔记：[Makefile基础](asic_lab_1/makefile.md)

### 6、 `git`

在本实验中，我们将使用`git`，这是最受欢迎的版本控制系统之一。强烈建议定期将您的更改推送到`GitHub`进行备份。有时可能会意外丢失本地数据。

#### 安装

安装教程来自：[如何在 Ubuntu 20.04 上安装 Git](https://zhuanlan.zhihu.com/p/137578868)

`git`软件包被包含在Ubuntu默认的软件源仓库中，并且可以使用 `apt`包管理工具安装。这是在 Ubuntu 上安装`git`最便利，最简单的方式。

以`sudo`权限用户身份运行下面的命令：

```
sudo apt update
sudo apt install git
```

运行下面的命令，打印 `git` 版本，验证安装过程：

```
git --version
```

#### 设置

**在git中配置用户名**

设置教程来自：
[在 Git 中设置用户名](https://docs.github.com/zh/get-started/getting-started-with-git/setting-your-username-in-git)

设置`git`用户名,然后确认已正确设置`git`用户名，成功后第二条命令会打印出我们设置的用户名。

```
git config --global user.name "Mona Lisa"
git config --global user.name
```

**在git中配置您的电子邮件地址**

设置教程来自：
[设置提交电子邮件地址](https://docs.github.com/zh/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address)

设置`git`电子邮件,然后确认已正确设置`git`电子邮件，成功后第二条命令会打印出我们设置的电子邮件。

```
git config --global user.email "YOUR_EMAIL"
git config --global user.email
```

**创建一个SSH密钥**

教程：
[生成新的 SSH 密钥并将其添加到 ssh-agent](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

如果您使用密码创建SSH密钥，则每次推送/拉取时都需要键入密码。我们建议将密码留空，但这是您的选择。

**将SSH密钥添加到您的GitHub帐户**

教程：
[新增 SSH 密钥到 GitHub 帐户](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

#### 测试

完成后，请确保您可以通过运行`ssh`对`GitHub`进行身份验证：

```
ssh -T git@github.com
```

如果正确配置，shell会显示以下内容：

```
Hi <YOUR GITHUB USERNAME>! You've successfully authenticated, but GitHub does not provide shell access.
```

#### 教程&要求

在本实验中，只需要掌握以下命令：

`git status`、`git add`、`git commit`、`git pull`、`git push`、`git clone`

如果愿意学习如何使用一些更强大的功能（`diff, blame, branch, log, mergetool, rebase, and many others`），它们可以大大提高生产力。

我的笔记：

#### `vim编辑器`

以`sudo`权限用户身份运行下面的命令：

```
sudo apt install vim
```

运行下面的命令，打印 `vim` 版本，验证安装过程：

```
git --version
```

## 实验二：仿真（Lab 2:Simulation）

### 1、Verilog语法回顾

一些合适的教程：[Verilog基础](asic_lab_2/SETP1_Verilog.md)

### 2、CAD软件

UCB使用的CAD软件是`Synopsys VCS`，鉴于在国内大概率没有教育许可证，改用开源的`Verilator`。

我的`Verilator`笔记：[Verilator入门](asic_lab_2/STEP2_Verilator.md)

