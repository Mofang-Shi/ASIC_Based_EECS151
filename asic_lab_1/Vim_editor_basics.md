# Vim编辑器基础教程

## 介绍

本教程来自`UCB EECS151 ASIC Lab1`推荐阅读的教程：[Interactive Vim tutorial](https://www.openvim.com/tutorial.html)

参考资料：[Vim编辑器常用命令](https://blog.csdn.net/zhang_yu_ling/article/details/103777714)

## 1.Two modes, `insert` and `normal`

`i,I` 更改为插入模式（insert mode）

`Esc` 切换到正常模式（normal mode）

## 2.Basic movement: `h`, `j`, `k`, and `l`

`h, j, k, l`  左、下、上、右移动

## 3.Word movement: `w`, `e`, `b`

`w` 移动到下一个单词的开头

`e` 移动到当前单词的结尾

`b` 移动到上一个单词的开头

`ge` 移动到前一个单词的结尾

`gg` 移动到缓冲区的开头

`g Esc` 取消移动

## 4.Number powered movement (e.g. `5w`)

`[n][action/movement]` 重复n次

`5w` 移动到五个个单词后的开头

`3x` 删除3个连续字符

## 5.Insert text repeatedly(e.g.`3iYes`)

`[n][i/I/A/a][words]`

`i,I,A,a` 当前光标处，行首插入，行末插入，光标后插入

`3iYes+Esc` 在当前光标处插入三遍yes

## 6.Find a character, `f` and `F`

`f[char]` 向后搜索<字母>并跳转到第一个匹配的位置

`F[char]` 向前搜索<字母>并跳转到第一个匹配的位置

`t[char]` 向后搜索<字母>并跳转到第一个匹配位置之前的字母

`T[char]` 向前搜索<字母>并跳转到第一个匹配位置之后的字母

## 7.Go to matching parentheses`%`

`%` 转到相应的括号

## 8.Go to start/end of line, `0` and `$`

`0或^` 移动到行头

`$` 移动到行尾

## 9.Find word under cursor, `*` and `#`

`*` 找到光标下单词的下一个出现

`#` 找到光标下单词的下一个出现

## 10.Goto line, g and G

`gg` 游标移动到第一行

`G` 游标移动到最后一行

`nG` 游标移动到第n行（如果默认没有显示行号，请先进入命令行模式，输入:set nu以显示行号）

`dG` 删除到文档结尾处

`d1G` 删除至文档首部

## 11. Search, /text with n and N

`/+<strings>+Enter` 向下查找（`n`下一个内容，`N`上一个内容，命令行模式下输入noh回车可取消搜索）

`?+<strings>+Enter` 向上查找

`\*`寻找游标所在处的单词

## 12.Insert new line, o and O

`o` 在当前行后插入一个新行

`O` 在当前行前插入一个新行

`cw` 替换从光标所在位置到一个单词的结尾字符

## 13.Removing a character, x and X

`x,X` 删除游标所在的字符

## 14. Replacing letter under cursor, r

`r+<char>` 将游标所在字母替换为指定字母

`R` 连续替换，直到按下Esc

## 15.Deleting, d

`Delete` 同x

`dd` 删除整行

`2dd` 向下删除2行，以此类推

`dw` 删除一个单词（不适用中文）

`daw`(delete a word) 删除一个单词

`d[n]w` 删除n个单词

`d$或D` 删除至行尾

`d^` 删除至行首

`dG` 删除到文档结尾处

`d1G` 删除至文档首部

## 16.Repetition with`.`

`.` 重复上一次的命令操作

## 17.Visual mode, v

## 18.Real Vim awaits
`:q!` 制退出vim，不保存

`:q` 退出vim

`:wq!` 强制保存并退出vim

`:w <File_Path>` 另存为

`:saveas <File_Path>` 另存为

`:x` 保存并退出vim

`:wq` 保存并退出vim

`:set nu` 显示行号

`:set shiftwidth=10` 设置缩进为10个字符，以此类推（输入Esc回到普通模式，再次尝试>>看缩进是否变化）

`:ce(center)` 本行内容居中

`:ri(right)` 本行内容居右

`:le(left)` 本行内容居左
