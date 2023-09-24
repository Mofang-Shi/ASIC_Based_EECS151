## 问题1：常见的终端任务

对于下面的1-6，提交生成所需结果所需的命令。对于1-4，尝试只生成所需的结果（没有无关信息）。

**1. 在`/usr/bin`中列出最近修改的5个项目。**

普通版：

```shell
shimofang@shimofang-virtual-machine:~$ cd /usr/bin
shimofang@shimofang-virtual-machine:/usr/bin$ ls -1t | head -5
zstdcat
zstdmt
ypdomainname
xzcat
xzcmp
```

没有无关信息版：

```shell
shimofang@shimofang-virtual-machine:~$ ls /usr/bin -1t | head -5
zstdcat
zstdmt
ypdomainname
xzcat
xzcmp

```

**2.`git`安装在哪个目录中？**

```shell
shimofang@shimofang-virtual-machine:~$ which git
/usr/bin/git
```

**3.显示实验室目录中的隐藏文件（题目替换为显示`/home/{your_username}`中的隐藏文件）**

```shell
shimofang@shimofang-virtual-machine:~$ ls -a
.              .bash_logout  Downloads         Picture                    Video
..             .bashrc       .lesshst          .profile
模板           .cache        .local            Public
桌面           .config       Music             snap
.bash_history  Doc           .pam_environment  .sudo_as_admin_successful
```

**4.安装了哪个版本的Vim？描述你是如何弄明白这一点的。**

使用版本查看命令：

```shell
shimofang@shimofang-virtual-machine:~$ vim --version
VIM - Vi IMproved 8.2 (2019 Dec 12, compiled Aug 18 2023 04:12:26)
包含补丁: 1-3995, 4563, 4646, 4774, 4895, 4899, 4901, 4919, 213
修改者 team+vim@tracker.debian.org
编译者 team+vim@tracker.debian.org
and more...
```

**5.将此实验室中的文件复制到/scratch，然后删除它。（题目替换为把以下命令生成的文件复制到/scratch，然后删除它）**

```
mkdir L1Q5
ls -1 > /home/{your_username}/L1Q5/list.txt
sort < /home/{your_username}/L1Q5/list.txt >  /home/{your_username}/L1Q5/list_sorted.txt
```

使用`cp`和`rm`：

```shell
shimofang@shimofang-virtual-machine:~$ cp -r /home/shimofang/L1Q5 /home/shimofang/scratch
shimofang@shimofang-virtual-machine:~$ ls /home/shimofang/scratch
list_sorted.txt  list.txt
shimofang@shimofang-virtual-machine:~$ rm -r /home/shimofang/scratch
shimofang@shimofang-virtual-machine:~$ ls /home/shimofang/scratch
ls: cannot access '/home/shimofang/scratch': No such file or directory
```

**6.运行`ping www.google.com`，暂停它，然后终止进程。然后在后台运行它，报告它的PID，然后杀死进程。**

暂停进程使用`ctrl+z`

```shell
shimofang@shimofang-virtual-machine:~$ ping www.google.com
PING www.google.com (98.159.108.57) 56(84) bytes of data.
^Z
[1]+  Stopped                 ping www.google.com
shimofang@shimofang-virtual-machine:~$ kill %1

[1]+  Stopped                 ping www.google.com
shimofang@shimofang-virtual-machine:~$ ping www.google.com &
[2] 9813
[1]   Terminated              ping www.google.com
shimofang@shimofang-virtual-machine:~$ ps
    PID TTY          TIME CMD
   9804 pts/0    00:00:00 bash
   9813 pts/0    00:00:00 ping
   9814 pts/0    00:00:00 ps
shimofang@shimofang-virtual-machine:~$ kill 9813
[2]+  Terminated              ping www.google.com
```

**7.运行顶部并报告平均CPU负载、最高CPU作业和使用的内存量（只需报告此问题的结果；您无需提供命令/如何获得它）。**

```shell
shimofang@shimofang-virtual-machine:~$ top

top - 01:43:46 up 10:46,  1 user,  load average: 0.09, 0.15, 0.17
Tasks: 285 total,   2 running, 283 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.5 us,  0.8 sy,  0.0 ni, 97.6 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3871.6 total,    167.9 free,   1297.1 used,   2406.5 buff/cache
MiB Swap:   2140.0 total,   2136.5 free,      3.5 used.   2282.0 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                              
   1250 shimofa+  20   0 4395076 275088 129524 R   3.3   6.9   7:03.90 gnome-shell                          
   9776 shimofa+  20   0  645044  61908  47320 S   1.0   1.6   0:01.64 gnome-terminal-                      
   9820 shimofa+  20   0   16304   4096   3200 R   1.0   0.1   0:00.40 top                                  
    584 root      20   0  320524   9088   7552 S   0.7   0.2   3:15.23 vmtoolsd                             
   9748 root      20   0       0      0      0 I   0.7   0.0   0:01.26 kworker/0:1-events                   
top - 01:44:25 up 10:47,  1 user,  load average: 0.24, 0.18, 0.18
Tasks: 285 total,   1 running, 284 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.7 us,  0.8 sy,  0.0 ni, 97.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3871.6 total,    167.6 free,   1297.5 used,   2406.5 buff/cache
MiB Swap:   2140.0 total,   2136.5 free,      3.5 used.   2281.6 avail Mem 
```

## 问题2：常见的编辑任务

对于下面的每个任务，描述您需要按的键（the keys you need to press）来完成文件`force_regs.ucli`中的操作。

### 缺失文件，暂时跳过（2023.9.24）


**1.删除5行**

**2.搜索文本时钟**

**3.将文本dut替换为device_under_test**

**4.跳到文件的末尾**

**5.转到42号线**

**6.重新加载文件（以防在另一个窗口中修改）**

**7.保存并退出**

## 问题3：正则表达式的乐趣

### 缺失文件，暂时跳过（2023.9.24）

对于每个正则表达式，提供基本模式和扩展模式（sed和sed -r）的答案。您可以使用多个命令来执行每个任务。对force_regs.ucli文件进行操作。

**1.将所有x的周围数字更改为角括号。例如，regx15xx79x变为reg<15><79>。提示：记住启用全局替换。**

**2.使文件中的每个数字都恰好为3位数字，并加了前导零（每行的最后0除外）。** 例如，第120/121行应为：

```
force -deposit rocketTestHarness.dut.Raven003Top_withoutPads.TileWrap.
... .io_tilelink_release_data.sync_w002r.rq002_wptr_regx000x.Q 0
force -deposit rocketTestHarness.dut.Raven003Top_withoutPads.TileWrap.
... .io_tilelink_release_data.fifomem.mem_regx015xx098x.Q 0
```

