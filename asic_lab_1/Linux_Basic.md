
# Linux基础

[TOC]

## 介绍

本教程来自`UCB EECS151 ASIC Lab1`推荐阅读的教程：Learning the Shell：[Learning the Shell](http://linuxcommand.org/lc3_learning_the_shell.php)

## 一、“Shell”是什么?

简而言之，Shell是一个**从键盘上获取命令并将其交给操作系统执行的程序**。在过去，它是Linux等类Unix系统上唯一可用的用户界面。如今，除了Shell等命令行界面（command line interfaces，CLI）外，我们还有图形用户界面（graphical user interfaces，GUI）。

在大多数Linux系统上，一个名为`bash`的程序（代表Bourne Again SHell，由Steve Bourne编写的原始Unix shell程序sh的增强版本）充当Shell程序。除了bash，还有其他适用于Linux系统的shell程序。这些包括：`ksh`、`tcsh`和`zsh`。

### 在终端（Terminal）键入/使用鼠标

打开一个终端窗口。我们应该看到的第一个东西是一个shell提示，其中包含我们的用户名和机器名称，后跟一个美元符号（$）。如下所示：

```shell
shimofang@shimofang-virtual-machine:~$ 
```

**向上箭头键**——上一个命令（Command history）

**向下箭头键**——回到空白行

**向左/右键**——移动光标

**使用鼠标**——复制文本

**超级用户（Superuser）**： 如果shell提示符的最后一个字符是`#`而不是`$`，则正在作为超级用户操作。这意味着拥有管理权限，可以删除或覆盖系统上的任何文件。
**除非绝对需要管理权限，否则不要作为超级用户操作！**

## 二、导航（Navigation）

这个部分将会使用到三个命令：`pwd`打印工作目录、`cd`更改目录、`ls`列表文件和目录

### `pwd`

我们所处的目录称为工作目录（Working directory）。要查看工作目录的名称，我们使用pwd命令：

```shell
shimofang@shimofang-virtual-machine:~$ pwd
/home/shimofang
```

当我们第一次登录Linux系统时，工作目录被设置为我们的主目录（home directory）。这就是我们放文件的地方。在大多数系统上，主目录将被称为`/home/user_name`，但根据系统管理员的奇思妙想，它可以是任何东西。

### `ls`

要列出工作目录中的文件，我们使用ls命令：

```shell
shimofang@shimofang-virtual-machine:~$ ls
公共的  模板  视频  图片  文档  下载  音乐  桌面  snap
```

### `cd`

要更改工作目录，我们使用cd命令：
`cd + 所需工作目录的路径名`

路径名可以指定两种不同的方式：`绝对路径名`或`相对路径名`。

**绝对路径名**从根目录开始，并逐个分支跟随树，直到所需目录或文件的路径完成。例如，您的系统上有一个目录，其中安装了大多数程序。目录的路径名是`/usr/bin`。这意味着从根目录（由路径名中的前导斜杠表示）有一个名为“usr”的目录，其中包含一个名为“bin”的目录。

```shell
shimofang@shimofang-virtual-machine:~$ cd /usr/bin
shimofang@shimofang-virtual-machine:/usr/bin$ pwd
/usr/bin
shimofang@shimofang-virtual-machine:/usr/bin$ ls
'['                                   mtr-packet
 aa-enabled                           mv
 aa-exec                              namei
 aa-features-abi                      nano
 aconnect                             nautilus
 acpi_listen                          nautilus-autorun-software
 add-apt-repository                   nautilus-sendto
 addpart                              nawk
 airscan-discover                     nc

and many more...
```

现在我们可以看到，我们已经将当前工作目录更改为/usr/bin，并且它充满了文件。注意shell提示是如何更改的吗？为了方便起见，它通常设置为**显示工作目录的名称**。

**相对路径名**从工作目录开始。为此，它使用几个特殊符号来表示文件系统树中的相对位置。

`.`——指工作目录本身、`..`——指工作目录的父目录

```shell
shimofang@shimofang-virtual-machine:~$ cd /usr/bin
shimofang@shimofang-virtual-machine:/usr/bin$ cd ..
shimofang@shimofang-virtual-machine:/usr$ cd ./bin
shimofang@shimofang-virtual-machine:/usr/bin$ 
```

**键入cd后不跟任何内容**——cd会将工作目录更改为我们的主目录。

**键入cd ~user_name**——cd会将工作目录更改为指定用户的主目录。

**键入cd-**——将工作目录更改为上一个目录。

### 关于文件名的重要事实

1、以句号字符开头的文件名被隐藏。除非我们用`ls -a`，否则ls不会列出它们。

2、Linux中的文件名和Unix一样，区分大小写。文件名“File1”和“file1”指的是不同的文件。

3、Linux没有像Windows系统那样的“文件扩展”概念。您可以以任何您喜欢的方式命名文件。但许多应用程序会关心文件扩展名。

4、虽然Linux支持可能包含嵌入式空格和标点符号的长文件名，但将标点符号限制为句号`.`、破折号`-`和下划线`_`。

5、最重要的是，**不要在文件名中嵌入空格**。如果您想表示文件名中单词之间的空格，请使用下划线字符。

## 三、浏览（Looking Around）

这个部分将会使用到三个命令：`ls`列表文件和目录、`less`查看文本文件、`file`对文件的内容进行分类

### `ls`

`ls`命令用于列出目录的内容。这可能是最常用的Linux命令。它可以以多种不同的方式使用。以下是一些例子：
| Command         | Result                                                                                     |
|-----------------|--------------------------------------------------------------------------------------------|
| ls              | 列出工作目录（working directory）中的文件                                                  |
| ls /bin         | 列出/bin目录（或指定的任何其他目录）中的文件                                               |
| ls -l           | 以长格式（long format）列出工作目录中的文件                                                |
| ls -l /etc /bin | 以长格式列出/bin目录和/etc目录中的文件                                                     |
| ls -la ..       | 以长格式列出工作目录父目录中的所有文件（即使名称以句号字符开头的文件，这些文件通常被隐藏） |

这些例子还指出了关于命令的一个重要概念。大多数命令的操作是这样的：

```shell
command -options arguments
   ↓        ↓        ↓
  ls       -l    /etc /bin
```

其中command是命令的名称，-options是对命令行为的一个或多个调整，参数（arguments）是命令操作的一个或多个对象。

在`ls`的情况下，我们看到`ls`是命令的名称，它可以有一个或多个选项，如`-a`和`-l`，并且它可以对一个或多个文件或目录进行操作。

### 关于长格式（Long Format）

```
-rw-------   1 me       me            576 Apr 17  2019 weather.txt
drwxr-xr-x   6 me       me           1024 Oct  9  2019 web_page
-rw-rw-r--   1 me       me         276480 Feb 11 20:41 web_site.tar
-rw-------   1 me       me           5743 Dec 16  2018 xmas_file.txt

----------  -------  -------     -------- ------------ -------------
    |          |        |            |         |             |
    |          |        |            |         |           文件名
    |          |        |            |         |
    |          |        |            |         +---       修改时间
    |          |        |            |
    |          |        |            +-------------   大小（以字节为单位）
    |          |        |   
    |          |        +--------------------------          组
    |          |
    |          +-----------------------------------        所有者
    |
    +----------------------------------------------       文件权限

```

`文件名（File Name）`文件或目录的名称。

`修改时间（Modification Time）`上次修改文件的时间。如果上次修改发生在过去六个月以上，则会显示日期和年份；否则会显示一天中的时间。

`大小（Size）`文件的大小（以字节为单位）

`组（Group）`除文件所有者外，还具有文件权限的组的名称。

`所有者（Owner）`拥有该文件的用户的名称。

`文件权限（File Permissions）`文件访问权限的表示。
第一个字符是文件的类型。`-`表示常规（普通）文件。`D`表示一个目录。

第二组三个字符代表文件所有者的读取、写入和执行（`r`、`w`、`x`）权限。

接下来的三个代表文件组的权利，最后三个代表授予其他人的权利。

###`less`

Less是一个让我们查看文本文件的程序。这非常方便，因为许多用于控制和配置Linux的文件都是人类可读的，只需键入`less file_name`即可调用。

启动`less`后，`less`将一次显示一页的文本文件。我们可以使用`Page Up`和`Page Down`键来浏览文本文件。为了使`less`退出，我们键入“q”。以下是一些`less`接受的命令：

| Command            | Action                                         |
|--------------------|------------------------------------------------|
| Page Up 或 b       | 向后滚动一页                                   |
| Page Down 或 space | 向前滚动一页                                   |
| G                  | 转到文本文件的末尾                             |
| 1G                 | 转到文本文件的开头                             |
| /characters        | 在文本文件中向前搜索第一个指定字符的出现的位置 |
| n                  | 重复之前的搜索                                 |
| h                  | 显示一个完整的列表——less的命令和选项           |
| q                  | 退出                                           |

### `file`

当我们在Linux系统中闲逛时，在我们尝试查看文件之前，确定文件包含哪种数据是有帮助的。这就是`file`命令进入的地方。`file`将检查一个文件，并告诉我们它是哪种文件。

要使用`file`程序，我们只需键入：

```shell
file name_of_file
```

`file`程序可以识别大多数类型的文件，例如：

| 文件类型                       | 描述                               | 是否可以作为文本查看         |
|--------------------------------|------------------------------------|------------------------------|
| ASCII text                     | 文本                               | 是                           |
| Bourne-Again shell script text | bash脚本                           | 是                           |
| ELF 64-bit LSB executable      | 可执行的二进制程序                 | 否                           |
| ELF 64-bit LSB shared object   | 共享图书馆                         | 否                           |
| GNU tar archive                | 磁带存档文件。存储文件组的常见方式 | 否，使用`tar`的`tvf`命令查看 |
| gzip compressed data           | 用gzip压缩的存档                   | 否                           |
| HTML document text             | 一个网页                           | 是                           |
| JPEG image data                | 压缩的JPEG图像                     | 否                           |
| PostScript document text       | PostScript文件                     | 是                           |
| Zip archive data               | 用zip压缩的内容                    | 否                           |

虽然看起来大多数文件不能作为文本查看，但我们将看到操作系统的许多功能都由文本配置文件（text configuration files）和shell脚本（shell scripts）控制。

## 四、一次Linux旅行（A Guided Tour）

对于下面列出的每个目录，请执行以下操作：

- `cd`进入每个目录。

- 使用`ls`列出目录的内容。

- 如果有有趣的文件，请使用`file`命令来确定其内容。

- 对于文本文件，请使用`less`来查看它们。

| 目录        | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /                | 文件系统开始的根目录（root directory）。根目录可能只包含子目录（subdirectories）。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| /boot            | 这是保存Linux内核（kernel）和引导加载程序文件（boot loader files）的地方。内核是一个名为**vmlinuz**的文件。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| /etc             |  `/etc`目录包含系统的配置文件(configuration files)。 `/etc`中的所有文件都应该是文本文件(text files)。                                                                                                                                                                                                                                                                                                                                                             |
| /bin, /usr/bin   | 这两个目录包含系统的大部分程序。`/Bin`目录具有系统操作所需的基本程序(essential programs)，而`/usr/bin`包含系统用户的应用程序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| /sbin, /usr/sbin | `sbin`目录包含用于系统管理(system administration)的程序，主要用于超级用户(superuser)。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| /usr             | `/Usr`目录包含各种支持用户应用程序的内容。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| /usr/local       | `/Usr/local`及其子目录用于安装用于本地机器上的软件和其他文件。这意味着不属于官方发行版（通常在`/usr/bin`）的软件在这里。当您在系统上找到要安装的有趣程序时，它们应该安装在`/usr/local`目录之中。大多数情况下，选择的目录是`/usr/local/bin`。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| /var             | `/Var`目录包含随着系统运行而更改的文件                                                                                                                                                                                                                                                                                                                                                                                         |
| /lib             | 共享库(shared libraries)（类似于其他操作系统中的**动态链接库,DLL**）保存在这里。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| /home            | `/Home`是用户保留个人工作的地方。一般来说，这是用户唯一允许写入文件的地方。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| /root            | 这是超级用户的主目录。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| /tmp             | `/Tmp`是一个程序可以在其中写入临时文件的目录。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| /dev             |`/dev`目录是一个特殊的目录，因为它并不真正包含通常意义上的文件。相反，它包含系统可用的设备。在Linux（如Unix）中，设备被视为文件。您可以像读取文件一样读取和写入设备。例如，`/dev/fd0`是第一个软盘驱动器，`/dev/sda`是第一个硬盘驱动器。内核理解的所有设备都在这里表示。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| /proc            | `/proc`目录也很特别,此目录不包含文件。事实上，这个目录实际上根本不存在。它是完全虚拟的。`/proc`目录包含内核本身的小窥视孔（little peep holes into the kernel itself）。此目录中有一组编号条目（numbered entries），对应于系统上运行的所有进程。此外，还有一些命名条目（named entries）允许访问系统的当前配置。其中许多条目都可以查看。尝试查看/`proc/cpuinfo`，此条目将告诉您内核对系统CPU的看法。                                                                                                                                                                                                                                                                                                                                                                                                   |
| /media           | 一个以特殊方式使用的普通目录。`/Media`目录用于挂载点（mount points）。不同的物理存储设备（如硬盘驱动器）在不同的地方连接到文件系统树（ file system tree）。这种将设备连接到树的过程称为安装（mounting）。要让设备可用，必须首先安装它。 |

关于以上目录更多信息请访问：[Second Lesson: A Guided Tour](http://linuxcommand.org/lc3_lts0040.php)

## 五、Manipulating Files

## 六、Working with Commands

## 七、I/O Redirection

## 八、Expansion

## 九、Permissions

## 十、Job Control
