
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

### `less`

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

### 我的Linux旅行

先访问一下`/boot`，列出其中的文件：

```shell
shimofang@shimofang-virtual-machine:~$ cd /boot
shimofang@shimofang-virtual-machine:/boot$ ls
config-6.2.0-26-generic      memtest86+.elf
config-6.2.0-33-generic      memtest86+_multiboot.bin
efi                          System.map-6.2.0-26-generic
grub                         System.map-6.2.0-33-generic
initrd.img                   vmlinuz
initrd.img-6.2.0-26-generic  vmlinuz-6.2.0-26-generic
initrd.img-6.2.0-33-generic  vmlinuz-6.2.0-33-generic
initrd.img.old               vmlinuz.old
memtest86+.bin

```

我想看看Linux内核是个什么东西：

```shell
shimofang@shimofang-virtual-machine:/boot$ file vmlinuz
vmlinuz: symbolic link to vmlinuz-6.2.0-33-generic
shimofang@shimofang-virtual-machine:/boot$ file vmlinuz-6.2.0-33-generic
vmlinuz-6.2.0-33-generic: regular file, no read permission

```

Shell告诉我`vmlinuz`是一个符号链接（symbolic links），指向`vmlinuz-6.2.0-33-generic`。于是尝试访问这个对象，结果被无情拒绝（因为是$不是#）。。。好吧，换个目录试试：

```shell
shimofang@shimofang-virtual-machine:/boot$ cd ..
shimofang@shimofang-virtual-machine:/$  cd /etc
shimofang@shimofang-virtual-machine:/etc$ ls
acpi                           hostid               polkit-1
adduser.conf                   hostname             ppp
alsa                           hosts                printcap
alternatives                   hosts.allow          profile


and many more...


fwupd                          NetworkManager       udisks2
gai.conf                       networks             ufw
gdb                            newt                 update-manager
gdm3                           nftables.conf        update-motd.d
geoclue                        nsswitch.conf        update-notifier
ghostscript                    openvpn              UPower


shimofang@shimofang-virtual-machine:/etc$ file hostid
hostid: data
shimofang@shimofang-virtual-machine:/etc$ file networks
networks: ASCII text
shimofang@shimofang-virtual-machine:/etc$ less networks
```

访问`hostid`，结果为`data`型。换一个`networks`，终于找到了`ASCII text`型！！！最后用用`less`命令查看。

## 五、操作文件（Manipulating Files）

这个部分将会使用到四个命令：

`cp` - 复制文件和目录

`mv` - 移动或重命名文件和目录

`rm` - 删除文件和目录

`mkdir` - 创建目录

这四个命令是最常用的Linux命令之一。它们是操作文件和目录的基本命令。

不过这些命令执行的一些任务如果使用图形文件管理器（graphical file manager）更容易完成。使用文件管理器，您可以将文件从一个目录拖放到另一个目录，剪切和粘贴文件，删除文件等。那么，为什么要使用这些旧的命令行程序呢？

答案是权力和灵活性。虽然使用图形文件管理器执行简单的文件操作很容易，但使用命令行程序可以更容易地执行复杂的任务。例如，您如何将所有HTML文件从一个目录复制到另一个目录，且只复制目标目录中不存在或比目标目录中版本更新的文件？使用文件管理器相当困难，但使用命令行非常简单：

```shell
shimofang@shimofang-virtual-machine:/$ cp -u *.html destination
```

### 通配符（Wildcards）

由于shell经常使用文件名，它提供了特殊字符来帮助您快速指定文件名组。这些特殊字符被称为通配符。通配符允许您根据字符模式选择文件名。下表列出了通配符及其选择的内容：

| 通配符        | 含义                                                                                                                                                                                                                     |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *             | 匹配任何字符                                                                                                                                                                                                             |
| ?             | 匹配任何单个字符                                                                                                                                                                                                         |
| [characters]  | 匹配作为集合字符成员中的任何字符。字符集也可以表示为 POSIX字符类，例如： `[:alnum:]`   字母数字字符； `[:alpha:]`   字母字符； `[:digit:]`   数字 `[:upper:]`；  大写字母字符 `[:lower:]`；  小写字母字符                                |
| [!characters] | 匹配任何不是字符集里的字符                                                                                                                                                                                               |

使用通配符，可以为文件名构建非常复杂的选择标准。以下是一些模式示例以及它们匹配的内容：

| 格式                          | 匹配内容                                          |
|-------------------------------|---------------------------------------------------|
| `*`                             | 所有文件名                                        |
| `g*`                            | 以字符“g”开头的所有文件名                         |
| `b*.txt`                        | 以字符“b”开头，以字符“.txt”结尾的所有文件名       |
| `Data???`                       | 任何以字符“Data”开头的文件名，后跟3个字符         |
| `[abc]*`                        | 任何以“a”或“b”或“c”开头的文件名，后跟任何其他字符 |
| `[[:upper:]]*`                  | 任何以一个大写字母开头的文件名                    |
| `BACKUP.[[:digit:]][[:digit:]]` | 以字符“BACKUP”开头的任何文件名，后跟正好两个数字  |
| `*[![:lower:]]`                 | 任何不以小写字母结尾的文件名                      |

### `cp`

`cp`程序复制文件和目录，它还可用于将多个文件（和/或目录）复制到不同的目录。

一些有用的`cp`用例及其可选项（-options）：

| 命令              | 结果                                                                                                        |
|-------------------|-------------------------------------------------------------------------------------------------------------|
| `cp file1 file2`   | 将`file1`的内容复制到`file2`中。如果`file2`不存在，则创建它；否则，`file2`将用`file1`的内容静默覆盖。                 |
| `cp -i file1 file2` | 如上所述。但由于指定了“`-i`”（交互式，interactive）选项，如果`file2`存在，则在用`file1`的内容覆盖之前会提示用户。 |
| `cp file1 dir1`     | 在目录`dir1`内将`file1`的内容复制到`dir1`的名为`file1`的文件中。                                                    |
| `cp -R dir1 dir2`   | 复制目录`dir1`的内容。如果目录`dir2`不存在，则创建它。否则，它会在目录`dir2`中创建一个名为`dir1`的目录。            |

### `mv`

`mv`命令根据其使用方式**移动**或**重命名**文件和目录。它要么将一个或多个文件移动到不同的目录，要么将重命名一个文件或目录。

一些有用的`mv`用例及其可选项（-options）：

| 命令                | 结果                                                                                         |
|---------------------|----------------------------------------------------------------------------------------------|
| `mv file1 file2`      | 如果`file2`不存在，则`file1`将重命名为`file2`。如果`file2`存在，其内容将静默替换为`file1`的内容。      |
| `mv -i file1 file2`   | 如上所述，由于指定了“-i”（交互式）选项，如果`file2`存在，则在用`file1`的内容覆盖之前会提示用户。 |
| `mv file1 file2 dir1` | 文件`file1`和`file2`被移动到目录`dir1`。如果`dir1`不存在，`mv`将以错误退出。                           |
| `mv dir1 dir2`        | 如果`dir2`不存在，则`dir1`将重命名为`dir2`。如果`dir2`存在，则目录`dir1`将在目录`dir2`内移动。           |

### `rm`

`rm`命令移除（删除）文件和目录。使用递归选项`-r`，`rm`也可用于删除目录。

一些有用的`rm`用例及其可选项（-options）：

| 命令              | 结果                                                                       |
|-------------------|----------------------------------------------------------------------------|
| `rm file1 file2`    | 删除`file1`和`file2`。                                                         |
| `rm -i file1 file2` | 如上所述，由于指定了“`-i`”（交互式）选项，因此在删除每个文件之前会提示用户。 |
| `rm -r dir1 dir2`   | 目录`dir1`和`dir2`及其所有内容将被删除。                                       |

### 谨慎使用`rm`

Linux没有undelete命令。一旦你用`rm`删除了一些东西，它就消失了。如果您不小心，特别是通配符，可以使用`rm`对系统造成巨大损害。

在将`rm`与通配符一起使用之前，请尝试这个有用的技巧：

**使用ls构建命令。通过这样做，您可以在删除文件之前看到通配符的效果。使用ls测试命令后，用向上箭头键调用命令，然后在命令中用rm代替ls。**

### `mkdir`

`mkdir`命令用于创建目录。

### 使用带有通配符的命令

| 命令                  | 结果                                                                                                                    |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------|
| `cp *.txt text_files`   | 将当前工作目录中以字符“`.txt`”结尾的所有文件复制到名为`text_files`的现有目录中。                                            |
| `mv dir1 ../*.bak dir2` | 将当前工作目录的父目录中的子目录`dir1`和以“`.bak`”结尾的所有文件移动到名为`dir2`的现有目录。                                  |
| `rm *~`                 | 删除当前工作目录中以字符“`~`”结尾的所有文件。一些应用程序使用此命名方案创建备份文件。使用此命令会将它们从目录中清除出来。 |

## 六、使用命令工作（Working with Commands）

这个部分将会使用到四个命令：

`type` - 显示有关命令类型的信息

`which` -找到一个命令

`help`  -显示shell内置的参考页面

`man`   - 显示在线命令参考

### 什么是“命令”？

命令可以是4种不同类型之一：

- **一个可执行程序（An executable program）**。就像我们在`/usr/bin`中看到的所有文件一样。在这个类别中，程序可以编译二进制文件，如用`C`和`C++`编写的程序，或用`shell`、`Perl`、`Python`、`Ruby`等脚本语言编写的程序。

- **内置在shell本身的命令（A command built into the shell itself）**。bash提供了许多内部称为shell内置的命令。例如，`cd`命令是一个内置的shell。

- **外壳功能（A shell function）**。这些是集成到环境（environment）中的微型外壳脚本。我们将在后面的课程中介绍配置环境和编写shell函数，但现在请注意它们的存在。

- **一个别名（An alias）**。我们可以定义自己的命令，由其他命令构建。这将在后面的课程中讨论。

### 识别命令——`type`

`type`命令是一个内置的shell，在给定特定命令名称的情况下，显示shell将执行的命令的类型（displays the kind of command the shell will execute）。

它的工作原理是这样的：

```shell
type command
```

其中“`command`”是我们要检查的命令的名称。

以下是一些例子：

```shell
shimofang@shimofang-virtual-machine:~$ type type
type is a shell builtin
shimofang@shimofang-virtual-machine:~$ type ls
ls is aliased to `ls --color=auto'
shimofang@shimofang-virtual-machine:~$ type clear
clear is hashed (/usr/bin/clear)
shimofang@shimofang-virtual-machine:~$ type cp
cp is /usr/bin/cp
```

我们看到了不同命令的结果。请注意，`ls`命令实际上是`ls --color=auto`命令的别名，现在我们知道为什么ls的输出以彩色显示了。

### 识别命令——`which`

有时一个系统上安装了多个版本的可执行程序。虽然这在桌面系统上并不常见，但在大型服务器上并不罕见。要确定给定可执行文件的确切位置，使用`which`命令：

```shell
shimofang@shimofang-virtual-machine:~$ which ls
/usr/bin/ls
```

`which`仅适用于可执行程序（executable programs），不适用于替代实际可执行程序的内置（builtins）或别名（aliases）。

### 命令文档——`help`

Bash为每个内置的shell都有一个帮助文档。要使用它，请键入“`help`”，后跟内置shell的名称。或者，我们可以添加`-m`选项来更改输出的格式。例如：

```shell
shimofang@shimofang-virtual-machine:~$ type rm
rm is /usr/bin/rm
shimofang@shimofang-virtual-machine:~$ help -m rm
bash: help: no help topics match `rm'.  Try `help help' or `man -k rm' or `info rm'.
shimofang@shimofang-virtual-machine:~$ type cd
cd is a shell builtin
shimofang@shimofang-virtual-machine:~$ help -m cd
NAME
    cd - Change the shell working directory.

SYNOPSIS
    cd [-L|[-P [-e]] [-@]] [dir]

DESCRIPTION
    Change the shell working directory.
    
    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
    
    The variable CDPATH defines the search path for the directory containing
    DIR.  Alternative directory names in CDPATH are separated by a colon (:).
    A null directory name is the same as the current directory.  If DIR begins
    with a slash (/), then CDPATH is not used.
    
    If the directory is not found, and the shell option `cdable_vars' is set,
    the word is assumed to be  a variable name.  If that variable has a value,
    its value is used for DIR.
    
    Options:
      -L	force symbolic links to be followed: resolve symbolic
    		links in DIR after processing instances of `..'
      -P	use the physical directory structure without following
    		symbolic links: resolve symbolic links in DIR before
    		processing instances of `..'
      -e	if the -P option is supplied, and the current working
    		directory cannot be determined successfully, exit with
    		a non-zero status
      -@	on systems that support it, present a file with extended
    		attributes as a directory containing the file attributes
    
    The default is to follow symbolic links, as if `-L' were specified.
    `..' is processed by removing the immediately previous pathname component
    back to a slash or the beginning of DIR.
    
    Exit Status:
    Returns 0 if the directory is changed, and if $PWD is set successfully when
    -P is used; non-zero otherwise.

SEE ALSO
    bash(1)

IMPLEMENTATION
    GNU bash, version 5.1.16(1)-release (x86_64-pc-linux-gnu)
    Copyright (C) 2020 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
```

当方括号`[]`出现在命令语法的描述中时，它们表示可选项。

垂直条形字符`|`表示相互排斥的项目。

许多可执行程序支持“`--help`”选项，该选项显示命令支持的语法（syntax）选项的描述，一些程序不支持，但无论如何都要尝试一下。例如：

```shell
shimofang@shimofang-virtual-machine:~$ type mkdir
mkdir is /usr/bin/mkdir
shimofang@shimofang-virtual-machine:~$ mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

Mandatory arguments to long options are mandatory for short options too.
  -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
  -p, --parents     no error if existing, make parent directories as needed
  -v, --verbose     print a message for each created directory
  -Z                   set SELinux security context of each created directory
                         to the default type
      --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                         or SMACK security context to CTX
      --help     display this help and exit
      --version  output version information and exit

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Report any translation bugs to <https://translationproject.org/team/>
Full documentation <https://www.gnu.org/software/coreutils/mkdir>
or available locally via: info '(coreutils) mkdir invocation'
```

### 正式文档——`man`

大多数用于命令行的可执行程序都提供了称为手册或手册页（manual or man page）的正式文档。使用一个名为`man`的特殊寻呼程序来查看它们。它被这样使用：

```shell
man program
```

其中“`program`”是查看命令的名称。手册页的格式略有不同，但通常包含标题、命令语法概要（synopsis of the command's syntax）、命令目的的描述（a description of the command's purpose）以及每个命令选项的列表和描述。手册页通常不包含示例，仅供参考，而不是教程。

在大多数Linux系统上，`man`使用`less`来显示手册页面，因此所有`less`的命令在显示页面时都可以使用。

### README和其他文档文件

系统上安装的许多软件包都有位于`/usr/share/doc`目录中的文档文件。其中大部分以纯文本格式（plain text format）存储，并且可以用`less`查看。一些文件是HTML格式的，可以使用网络浏览器（web browser）查看。我们可能会遇到一些以“`.gz`”扩展名结尾的文件。这表明它们已被`gzip`压缩程序压缩。Gzip包包括一个称为`zless`的特殊`less`版本，该版本将显示gzip压缩文本文件的内容。

## 七、I/O重定向（I/O Redirection）

在本课中，我们将探索命令行程序（command line programs）使用的称为输入/输出重定向（I/O Redirection）的强大功能。正如我们所看到的，许多命令（如`ls`）在显示器上打印其输出。然而，情况不必如此。通过使用一些特殊符号，我们可以将许多命令的输出重定向（redirect）到文件、设备，甚至重定向到其他命令的输入。

### 标准输出

大多数显示结果的命令行程序通过将其结果发送到称为标准输出（standard output）的设施来执行此操作。默认情况下，标准输出将其内容定向到显示器。要将标准输出重定向到文件，使用“`>`”字符：

```shell
shimofang@shimofang-virtual-machine:~/doc$ cd /home/shimofang/doc
shimofang@shimofang-virtual-machine:~/doc$ mkdir Linux_Basics
shimofang@shimofang-virtual-machine:~/doc$ ls
Linux_Basics
shimofang@shimofang-virtual-machine:~/doc$ cd
shimofang@shimofang-virtual-machine:~$ ls
公共的  模板  视频  图片  下载  音乐  桌面  doc  snap
shimofang@shimofang-virtual-machine:~$ ls > /home/shimofang/doc/Linux_Basics/file_list.txt
shimofang@shimofang-virtual-machine:~$ cd /home/shimofang/doc/Linux_Basics
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ ls
file_list.txt
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ less file_list.txt
```
ls -l `which cp` > “/home/shimofang/Doc/Linux_Basics/file with space.txt”
每次重复上述命令时，`file_list.txt`都会用命令`ls`的输出从头开始覆盖。为了将新结果附加到文件中，我们使用“`>>`”。当附加结果时，新结果将添加到文件的末尾，从而使每次重复命令时文件更长。如果我们尝试附加重定向的输出时文件不存在，则将创建该文件。

### 标准输入

许多命令可以接受来自称为标准输入（standard input）的设施的输入。默认情况下，标准输入从键盘获取其内容，但与标准输出一样，它可以被重定向。要从文件而不是键盘重定向标准输入，使用“`<`”字符：

```shell
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ sort < file_list.txt > sorted_file_list.txt
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ ls
file_list.txt  sorted_file_list.txt
```

正如我们所看到的，命令可以同时重定向其输入和输出。请注意，重定向的顺序并不重要。唯一的要求是重定向运算符（“`<`”和“`>`”）必须出现在命令中的其他选项（-options）和参数（arguments）之后。

### 管道（Pipelines）

我们可以用I/O重定向做的最有用和最强大的事情是将**多个命令连接在一起，以形成所谓的管道（Pipelines）**。对于管道，一个命令的标准输出被输入到另一个命令的标准输入中。这里有一个非常有用的例子：

```shell
shimofang@shimofang-virtual-machine:~$ ls -l | less
```

在本例中，`ls`命令的输出被输入到`less`。通过使用这个“`| less`”技巧，我们可以使任何命令具有滚动的输出。

以下是一些可以尝试的例子：

| 命令                           | 作用                                             |
|--------------------------------|--------------------------------------------------|
| `ls -lt \| head`                 | 显示当前目录中的10个最新文件                     |
| `du \| sort -nr`                 | 显示目录列表以及它们消耗的空间，从最大到最小排序 |
| `find . -type f -print \| wc -l` | 显示当前工作目录及其所有子目录中的文件总数。     |

### 过滤器（Filters）

管道中经常使用的一种程序被称为过滤器（Filters）。过滤器接受标准输入（standard input）并对其进行操作，并将结果发送到标准输出。通过这种方式，它们可以组合起来，以强大的方式处理信息。以下是一些可以充当过滤器的常见程序：

| 程序 | 作用                                                                                                                             |
|------|----------------------------------------------------------------------------------------------------------------------------------|
| sort | 对标准输入进行排序，然后在标准输出上输出排序结果。                                                                               |
| uniq | 给定标准输入中排序的数据流，它会删除重复的数据行（即确保每行都是唯一的）。                                                       |
| grep | 检查它从标准输入收到的每行数据，并输出包含指定字符模式（specified pattern of characters）的每行。                                |
| fmt  | 从标准输入中读取文本，然后在标准输出上输出格式化文本（formatted text）。                                                         |
| pr   | 从标准输入中获取文本输入，并将数据拆分为带有分页符、页眉和页脚的页面，以准备打印。                                               |
| head | 输出其输入的前几行。有助于获取文件的标头。                                                                                       |
| tail | 输出其输入的最后几行。适用于从日志文件中获取最新条目等。                                                                         |
| tr   | 翻译字符。可用于执行大写/小写转换或将行终止字符从一种类型更改为另一种类型（例如，将DOS文本文件转换为Unix风格的文本文件）等任务。 |
| sed  | 流编辑器。可以进行比tr更复杂的文本翻译                                                                                           |
| awk  | 为构建过滤器而设计的整个编程语言。非常强大。                                                                                     |

### 一些例子

1.**从命令行打印。** Linux提供了一个名为`lpr`的程序，该程序接受标准输入并将其发送到打印机。它经常与管道和过滤器（pipes and filters）一起使用。例如：

```shell
cat poorly_formatted_report.txt | fmt | pr | lpr
cat unsorted_list_with_dupes.txt | sort | uniq | pr | lpr
```

在第一个示例中，我们使用`cat`读取文件并将其输出到标准输出，该输出被输送到`fmt`的标准输入中。`fmt`将文本格式化为整洁的段落，并将其输出到标准输出中，该输出被输送到`pr`的标准输入中。`pr`将文本整齐地拆分为页面并输出到标准输出，该输出被输送到`lpr`的标准输入中。`lpr`将其标准输入并将其发送到打印机。

第二个示例从包含重复条目的未排序数据列表开始。首先，`cat`将列表发送到排序中，对其进行排序`sort`，并将其输入`uniq`，以删除任何重复项。下一个`pr`和`lpr`用于分页和打印列表。

2.**查看`tar`文件的内容。** 您通常会看到软件作为压缩的tar文件分发。这是一个传统的Unix风格的磁带存档文件（用tar创建），已用gzip压缩。您可以通过其传统文件扩展名“`.tar.gz`”或“`.tgz`”来识别这些文件。可以使用以下命令在Linux系统上查看此类文件的目录：

```shell
tar tzvf name_of_file.tar.gz | less
```

## 八、扩展（Expansion）

每次我们键入命令行并按回车键时，bash在执行命令之前都会对文本执行多个过程。我们已经看到了几个例子，一个简单的字符序列（例如“*”）对shell有很多意义。实现这一目标的过程被称为扩展（expansion）。通过扩展，我们键入一些东西，在shell作用于它之前，它被扩展为其他东西。为了演示我们的意思，让我们看看`echo`命令。`echo`是一个内置的shell，可以在标准输出上打印出其文本参数：

```shell
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ echo I am mofang
I am mofang
```

传递给`echo`的任何参数都会显示。让我们试试另一个例子：

```shell
shimofang@shimofang-virtual-machine:~/doc/Linux_Basics$ echo *
file_list.txt sorted_file_list.txt
```

为什么`echo`没有打印“`*`”？

通配符`*`意味着匹配文件名中的任何字符，但我们在最初的讨论中没有看到的是shell是如何做到这一点的。简单的答案是，在执行`echo`命令之前，shell将`*`扩展为其他东西（在本例中，是当前工作目录中文件的名称）。当按下回车键时，shell会在执行命令之前自动展开命令行上的任何符合要求的字符，因此`echo`命令不会打印`*`，只有其扩展结果。知道这一点后，我们可以看到`echo`命令的行为是符合预期的。

### 路径名扩展

通配符工作的机制称为路径名扩展（pathname expansion）。如果我们尝试我们在早期课程中使用的一些技术，我们将看到它们确实是扩展。给定一个看起来像这样的主目录：

```shell
shimofang@shimofang-virtual-machine:~$ ls
模板  桌面  Doc  Downloads  Music  Picture  Public  snap  Video
```

我们可以看见：
```shell
shimofang@shimofang-virtual-machine:~$ echo D*
Doc Downloads
shimofang@shimofang-virtual-machine:~$ echo *s
Downloads
shimofang@shimofang-virtual-machine:~$ echo [[:upper:]]*
Doc Downloads Music Picture Public Video
shimofang@shimofang-virtual-machine:~$ echo /usr/*/share
/usr/local/share
shimofang@shimofang-virtual-machine:~$ ls D*
Doc:
Linux_Basics

Downloads:
```

### Tilde Expansion

波浪号字符（“`~`”）具有特殊的含义。当在单词开头使用时，它会扩展到指定用户的主目录的名称（expands into the name of the home directory of the named user），如果没有命名用户，则扩展为当前用户的主目录：

```shell
shimofang@shimofang-virtual-machine:~$ echo ~
/home/shimofang
shimofang@shimofang-virtual-machine:~$ echo ~shimofang
/home/shimofang
shimofang@shimofang-virtual-machine:~$ echo ~shiyaofang
~shiyaofang
```

### 算术拓展

shell允许通过扩展执行算术。这允许我们使用shell提示符作为计算器：

```shell
$((expression))
```

一些例子：

```shell
shimofang@shimofang-virtual-machine:~$ echo $((2 + 2))
4
shimofang@shimofang-virtual-machine:~$ echo $((2^3/5+12))
14
shimofang@shimofang-virtual-machine:~$ echo $((99.3))
bash: 99.3: syntax error: invalid arithmetic operator (error token is ".3")
shimofang@shimofang-virtual-machine:~$ echo $((100/99))
1
shimofang@shimofang-virtual-machine:~$ echo $(($((5**2)) * 3))
75
shimofang@shimofang-virtual-machine:~$ echo Five divided by two equals $((5/2))
Five divided by two equals 2

```

### Brace Expansion

我们可以从包含大括号的模式创建多个文本字符串。这里有一个例子：

```shell
shimofang@shimofang-virtual-machine:~$ echo Front-{A,B,C}-Back
Front-A-Back Front-B-Back Front-C-Back
shimofang@shimofang-virtual-machine:~$ echo 我{上午,中午,下午}在睡觉
我上午在睡觉 我中午在睡觉 我下午在睡觉
```

要展开大括号的模式可能包含称为序言（preamble）的开头部分（leading portion）和称为后记（trailing）的尾部部分（postscript）。括号表达式本身可以包含逗号`,`分隔的字符串列表，也可以包含整数或单个字符的范围。该模式可能不包含嵌入式空格（embedded whitespace）。

使用一系列整数的示例：

```shell
shimofang@shimofang-virtual-machine:~$ echo 伞兵{1..3}号
伞兵1号 伞兵2号 伞兵3号
shimofang@shimofang-virtual-machine:~$ echo Number_{5..1}
Number_5 Number_4 Number_3 Number_2 Number_1
```

反向顺序的字母：

```shell
shimofang@shimofang-virtual-machine:~$ echo {Z..A}
Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
```

Brace Expansion可以嵌套：

```shell
shimofang@shimofang-virtual-machine:~$ echo a{A{1,2},B{3,4}}b
aA1b aA2b aB3b aB4b
```

那么这有什么好处呢？最常见的应用是**制作要创建的文件或目录列表**。例如，如果我们是一名摄影师，并且有大量想要组织成几年和几个月的图像，我们可能做的第一件事就是创建一系列以数字“年-月”格式命名的目录。这样，目录名称将按时间顺序排序:

```shell
shimofang@shimofang-virtual-machine:~$ cd /home/shimofang/P*e
shimofang@shimofang-virtual-machine:~/Picture$ mkdir Photos_tset
shimofang@shimofang-virtual-machine:~/Picture$ cd P*
shimofang@shimofang-virtual-machine:~/Picture/Photos_tset$ mkdir {2020..2023}-{1..12}
shimofang@shimofang-virtual-machine:~/Picture/Photos_tset$ ls
2020-1   2020-2  2020-6  2021-1   2021-2  2021-6  2022-1   2022-2  2022-6  2023-1   2023-2  2023-6
2020-10  2020-3  2020-7  2021-10  2021-3  2021-7  2022-10  2022-3  2022-7  2023-10  2023-3  2023-7
2020-11  2020-4  2020-8  2021-11  2021-4  2021-8  2022-11  2022-4  2022-8  2023-11  2023-4  2023-8
2020-12  2020-5  2020-9  2021-12  2021-5  2021-9  2022-12  2022-5  2022-9  2023-12  2023-5  2023-9
```

### 参数扩展（Parameter Expansion）

这是一个在shell脚本中比直接在命令行上更有用的功能。它的许多功能都与系统存储小块数据并给每个块命名的能力有关。许多这样的块，更恰当地称为变量（variables），可供我们检查。例如，名为“`USER`”的变量包含我们的用户名。要调用参数扩展并显示USER的内容，我们将这样做：

```shell
shimofang@shimofang-virtual-machine:~$ echo $USER
shimofang
```

要查看可用变量的列表，请尝试以下方法：

```shell
shimofang@shimofang-virtual-machine:~$ printenv | less
```

对于其他类型的扩展，如果我们键入错误的模式，扩展将不会发生，`echo`命令将简单地显示键入错误的模式。使用参数扩展，如果我们拼错变量的名称，扩展仍将发生，但将导致空字符串。

### 命令替换（Command Substitution）

命令替换允许我们使用命令的输出作为扩展：

```shell
shimofang@shimofang-virtual-machine:~$ echo $(ls)
模板 桌面 Doc Downloads Music Picture Public snap Video
shimofang@shimofang-virtual-machine:~$ ls -l $(which cp)
-rwxr-xr-x 1 root root 141824  2月  8  2022 /usr/bin/cp
```

在这里，我们将`which cp`作为参数的结果传递给`ls`命令，从而获得`cp`程序的列表，而不必知道其完整的路径名。我们不仅限于简单的命令。可以使用整个管道（Entire pipelines）（仅显示部分输出）：

```shell
shimofang@shimofang-virtual-machine:~$ file $(ls /usr/bin/* | grep bin/zip)
/usr/bin/zip:        ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=f4e3c129a9a184aecb256650d23ed3d92bcd60db, for GNU/Linux 3.2.0, stripped
/usr/bin/zipcloak:   ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=754f1c0c2e6121523bd6aa727edda9ba78a412bc, for GNU/Linux 3.2.0, stripped
/usr/bin/zipdetails: Perl script text executable
/usr/bin/zipgrep:    POSIX shell script, ASCII text executable
```

在本例中，管道的结果成为文件命令的参数列表。在较旧的shell程序中有一个命令替换的替代语法，bash也支持该语法。它使用反向引号而不是美元符号和括号：

```shell
shimofang@shimofang-virtual-machine:~$ ls -l `which cp`
-rwxr-xr-x 1 root root 141824  2月  8  2022 /usr/bin/cp
```

### 引用（Quoting）

观察示例：

```shell
shimofang@shimofang-virtual-machine:~$ echo this is a     test
this is a test
shimofang@shimofang-virtual-machine:~$ echo The total is $100.00
The total is 00.00
```

在第一个示例中，shell的单词拆分从`echo`命令的参数列表中删除了额外的空格。

在第二个示例中，参数扩展用空字符串替换了“$1”的值，因为它是一个未定义的变量。shell提供了一种称为引用（quoting）的机制，以选择性地抑制不需要的扩展（suppress unwanted expansions）。

**双引号（Double Quotes）**
如果我们把文本放在双引号中，shell使用的所有特殊字符都会失去其特殊意义，并被视为普通字符。例外是“$”、“\”（反斜杠）和“`”（反引号）。这意味着单词拆分、路径名扩展、波浪号扩展和大括号扩展被抑制，但参数扩展、算术扩展和命令替换仍然被执行。

使用双引号，我们可以处理**包含嵌入式空格**的文件名。想象一下，我们是一个名为two words.txt的文件的不幸受害者。如果我们试图在命令行上使用它，单词拆分将导致将其视为两个单独的参数，而不是所需的单个参数。

**Q：如何创建带有空格的文件？**

现在我们不必一直输入那些讨厌的双引号了。请记住，参数扩展、算术扩展和命令替换仍然在双引号中进行：

```shell
shimofang@shimofang-virtual-machine:~$ echo "$USER $((2+2))"
shimofang 4
shimofang@shimofang-virtual-machine:~$ echo $USER $((2+2))
shimofang 4
```

我们应该花点时间看看双引号对命令替换的影响。首先，让我们更深入地看看单词拆分是如何工作的（how word splitting works）。在我们之前的例子中，我们看到了单词拆分如何删除文本中的额外空格：

```shell
shimofang@shimofang-virtual-machine:~$ echo this is a     test
this is a test
```

默认情况下，单词拆分查找空格、制表符和换行符（换行符）的存在，并将其视为单词之间的分隔符。这意味着未引用的空格、制表符和换行符不被视为文本的一部分。它们仅作为分隔符。由于它们将单词分成不同的参数，我们的示例命令行包含一个命令，后跟四个不同的参数。如果我们添加双引号：

```shell
shimofang@shimofang-virtual-machine:~$ echo "this is a     test"
this is a     test
```

单词拆分被抑制，嵌入的空格不被视为分隔符，而是它们成为参数的一部分。添加双引号后，我们的命令行将包含一个命令，后跟一个参数。换行符被单词拆分机制视为分隔符。

**单引号（Single Quotes）**

当我们需要抑制所有扩展时，我们使用单引号。以下是未引用、双引号和单引号的比较：

```shell
shimofang@shimofang-virtual-machine:~$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/shimofang/*.txt a b foo 4 shimofang
shimofang@shimofang-virtual-machine:~$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt {a,b} foo 4 shimofang
shimofang@shimofang-virtual-machine:~$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```
### 转义字符（Escaping Characters）

有时我们只想引用一个字符。要做到这一点，我们可以在字符之前加反斜杠`\`，在此上下文中，反斜杠被称为转义字符。这通常是在双引号内完成的，以便有选择地防止扩展。

```shell
shimofang@shimofang-virtual-machine:~$ echo "The balance for user $USER is: \$5.00"
The balance for user shimofang is: $5.00
```

使用转义来消除文件名中字符的特殊含义也很常见。例如，可以在文件名中使用通常对shell具有特殊意义的字符。这些将包括“`$`”、“`!`”、“`&`”等。要在文件名中包含一个特殊字符，我们可以这样做：

```shell
mv bad\&filename good_filename
```

要允许反斜杠字符出现，请键入“\\\”来转义它。请注意，在单引号中，反斜杠失去了其特殊含义，并被视为普通字符。

### 反斜线技巧（Backslash Tricks）

如果我们查看[GNU项目](http://www.gnu.org/)编写的任何程序的手册页，我们会发现，除了由破折号和单个字母组成的命令行选项外，还有以两个破折号开头的长选项名称。例如，以下是等价的：

```
ls -r
ls --reverse
```

为什么支持两者？

短形式适用于命令行上的懒惰打字员，长形式主要适用于脚本（scripts），尽管一些选项可能仅以长形式提供。有时，当选项模糊不清时，**最好使用长选项**。在编写需要最大可读性的脚本时，这尤其有用。

使用长表单选项可以使单个命令行非常长。为了解决这个问题，我们可以使用反斜杠让shell忽略像这样的换行符：

```
ls -l \
   --reverse \
   --human-readable \
   --full-time
```

以这种方式使用反斜杠允许我们在命令中嵌入换行符。请注意，要使这个技巧发挥作用，必须在反斜杠后立即键入换行。

反斜杠也用于在我们的文本中插入特殊字符。这些被称为反斜杠转义字符：

| 转义字符 | 名字     | 可能的用途                       |
|----------|----------|----------------------------------|
| \n       | 新行     | 文本中添加空白行                 |
| \t       | 制表符   | 在文本中插入水平制表符           |
| \a       | 警告     | 发出我们的终端蜂鸣声             |
| \\       | 反斜线   | 插入反斜杠                       |
| \f       | formfeed | 将此发送到我们的打印机会弹出页面 |

使用反斜杠转义字符非常常见。这个想法首次出现在C编程语言中。今天，shell、C++、Perl、python、awk、tcl和许多其他编程语言都使用这个概念。将echo命令与-e选项（启用反斜杠转义的解释）一起使用：

```shell
shimofang@shimofang-virtual-machine:~$ echo -e "Inserting several blank lines\n\n\n"
Inserting several blank lines
-------line-------
-------line-------
-------line-------
shimofang@shimofang-virtual-machine:~$ echo -e "Words\tseparated\tby\thorizontal\ttabs."
Words	separated	by	horizontal	tabs.

```

## 九、Permissions

## 十、Job Control
