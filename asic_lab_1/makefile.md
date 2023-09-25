# Makefile基础

## 介绍

本教程来自`UCB EECS151 ASIC Lab1`推荐阅读的教程：[A Simple Makefile Tutorial](https://cs.colby.edu/maxwell/courses/tutorials/maketutor/)

额外的阅读资料（个人觉得读这个更好）：[Makefile教程](https://blog.csdn.net/weixin_38391755/article/details/80380786)
## 一个示例（来自`Lab1`）

让我们看看一个简单的makefile，来解释一些关于它们如何工作的事情。如果您查看某的文本编辑器中提供的文件夹中的`Makefile`，您可以看到以下行：

```Makefile
output_name = force_regs.random.ucli

$(output_name): force_regs.ucli
    awk 'BEGIN{srand();}{if ($$1 != "") { print $$1,$$2,$$3,int(rand()*2)}}' $< > $@

clean:
    rm -f $(output_name)
```

虽然这可能看起来像很多随机字符，但让我们浏览一下它的每个部分，真的没有那么复杂。

Makefile通常由规则（rules）组成，这些规则告诉`Make`如何执行一组命令，从一组依赖项（dependencies）构建一组目标（targets）。规则通常具有以下结构：

```
targets: dependencies
    commands
```

**Makefiles中的缩进是制表符`Tab`，而不是空格，这一点非常重要**。

上述Makefile中的两条规则具有干净和输出名称的目标。在这里，输出名称是Makefile中变量的名称，这意味着它可以从命令行覆盖（overwritten）。这可以通过以下命令完成：

```shell
make output_name=foo.txt
```

这将导致输出写入`foo.txt`文件中。

通常，每当其依赖项更新于其自身目标时，规则都会运行，因此通过编辑/更新`foo.txt`文件（包括通过触摸命令，touch command），可以重新生成输出名称目标。这与`bash`脚本不同。

在输出名称目标中，`awk`命令有一堆`$`字符。这是因为在正常的`awk`中，变量名是`1$`，`2$`，然后在makefile中，你必须转义这些变量名才能让它们正常工作。在`Make`中，转义使用`$`而不是`\`。

awk脚本之后的其他字符也是要制作的特殊字符。`$<`是该目标的第一个依赖项，`>`只是重定向`awk`的输出，`$@`是目标本身的名称。这允许用户创建可重用的文件，因为您正在依赖项上操作，并将结果输出到您自己的目标名称中。

## 一个简单的Makefile教程（来自推荐阅读）

Makefiles是组织代码编译（code compilation）的简单方法。本教程甚至没有触及使用make的可能性，而是作为入门指南，以便可以快速轻松地为中小型项目创建自己的makefile。

### 一个简单的例子

让我们从以下三个文件开始，`hellomake.c`、`hellofunc.c`和`hellomake.h`（C语言头文件），它们将分别代表一个典型的**主程序**、一个单独文件中的**一些功能代码**和一个**包含文件**。

`hellomake.c`

```C
#include <hellomake.h>

int main() {
  // call a function in another file
  myPrintHelloMake();

  return(0);
}
```

`hellofunc.c`

```C
#include <stdio.h>
#include <hellomake.h>

void myPrintHelloMake(void) {

  printf("Hello makefiles!\n");

  return;
}
```

`hellomake.h`

```C
/*
example include file
*/

void myPrintHelloMake(void);
```

通常，将通过执行以下命令来编译此代码集合：

```shell
gcc -o hellomake hellomake.c hellofunc.c -I.
```

这里编译了两个`.c`文件`hellomake.c`、`hellofunc.c`，并命名了可执行文件`hellomake`。`-I.`的作用是以便`gcc`在当前目录（.）中查找包含的头文件`hellomake.h`。

如果没有makefile，测试/修改/调试周期（test/modify/debug cycle）的典型方法是使用终端中的向上箭头返回到上一个编译命令，这样您就不必每次都键入它，特别是当在混合了几个`.c`文件后。

不幸的是，这种编译方法有两个缺点。首先，如果您丢失了编译命令或切换计算机，您必须从头开始重新键入它。其次，如果您只对一个`.c`文件进行更改，那么每次重新编译它们也是耗时且低效的。

此时就能用makefile做什么了！可以创建的最简单的makefile例如：

**Makefile1**

```Makefile
hellomake: hellomake.c hellofunc.c
     gcc -o hellomake hellomake.c hellofunc.c -I.
```

如果您将此规则放入名为`Makefile`或`makefile`的文件中，然后在命令行上键入`make`，它将执行编译命令，就像您在`makefile`中写入的那样。

请注意，`make`没有参数（arguments ）会执行文件中的第一条规则。此外，通过`:`后第一行的文件列表，`make`知道如果这些文件中的任何一个发生变化，则需要执行`hellomake`规则。

需要注意的一件非常重要的事情是，在makefile中的gcc命令之前有一个`Tab`，任何命令的开头都必须有一个`Tab`。

如此，我们已经解决了重复使用向上箭头的问题。然而，该系统在汇编最新更改方面仍然没有效率。

**Makefile2**

```Makefile
CC=gcc
CFLAGS=-I.

hellomake: hellomake.o hellofunc.o
     $(CC) -o hellomake hellomake.o hellofunc.o

```

现在我们定义了一些常数`CC`和`CFLAGS`。`宏CC`（macro CC）是使用的C编译器，`CFLAGS`是传递给编译命令的标志列表。

通过将对象文件`hellomake.o`和`hellofunc.o`放在依赖列表和规则（dependency list and in the rule）中，`make`知道它必须首先单独编译`.c`版本，然后构建可执行的`hellomake`。

补充一下关于gcc的知识，gcc编译C源码有四个步骤：

- 源文件`.c`和头文件`.h`的**预处理**
- 处理源文件`.i`的**编译**
- 汇编源文件`.s`的**汇编**
- 目标文件`.o`的**链接**
- 生成可执行文件

对于大多数小规模项目来说，使用这种形式的makefile就足够了。但是如果要更改`hellomake.h`，make不会重新编译`.c`文件，即使它们需要重新编译。

为了解决这个问题，我们需要告诉`make`所有`.c`文件都依赖于某些`.h`文件。我们可以通过编写一个简单的规则(rules)并将其添加到makefile来做到这一点。

**Makefile3**

```Makefile
CC=gcc
CFLAGS=-I.
DEPS = hellomake.h

%.o: %.c $(DEPS)
    $(CC) -c -o $@ $< $(CFLAGS)

hellomake: hellomake.o hellofunc.o 
    $(CC) -o hellomake hellomake.o hellofunc.o 
```

首先创建`宏DEPS`，这是`.c`文件所依赖的`.h`文件集。然后，我们定义了一个适用于所有以`.o`后缀结尾的文件的规则。

该规则规定，`.o`文件取决于文件的`.c`版本和`DEPS宏`中包含的`.h`文件。然后，要生成`.o`文件，需要使用`CC宏`中定义的编译器编译`.c`文件。`-C`标志表示生成对象文件（object file），`-o $@`表示将编译的输出放在`：`左侧命名的文件中（`%.o`），`$<`是依赖项列表中的第一个项目（`%.c`），`CFLAGS宏`定义如上例。

**Makefile4**

```Makefile
CC=gcc
CFLAGS=-I.
DEPS = hellomake.h
OBJ = hellomake.o hellofunc.o 

%.o: %.c $(DEPS)
    $(CC) -c -o $@ $< $(CFLAGS)

hellomake: $(OBJ)
    $(CC) -o $@ $^ $(CFLAGS)
```

作为最后的简化，让我们使用特殊的宏`$@`和`$^`，它们分别在`:`的左右两侧，以使整体编译规则更加通用。在上面的示例中，所有包含文件`.h`都应列为`宏DEPS`的一部分，所有对象文件`.o`都应列为`宏OBJ`的一部分。

如果在开始将我们的`.h`文件放在`/include`中，将我们的源代码（ source code）放在`src`目录中，并将一些本地库（local libraries）放在`lib`目录中呢，并隐藏`.o`文件，如下所示：

**Makefile5**

```Makefile
IDIR =../include
CC=gcc
CFLAGS=-I$(IDIR)

ODIR=obj
LDIR =../lib

LIBS=-lm

_DEPS = hellomake.h
DEPS = $(patsubst %,$(IDIR)/%,$(_DEPS))

_OBJ = hellomake.o hellofunc.o 
OBJ = $(patsubst %,$(ODIR)/%,$(_OBJ))


$(ODIR)/%.o: %.c $(DEPS)
    $(CC) -c -o $@ $< $(CFLAGS)

hellomake: $(OBJ)
    $(CC) -o $@ $^ $(CFLAGS) $(LIBS)

.PHONY: clean

clean:
    rm -f $(ODIR)/*.o *~ core $(INCDIR)/*~ 
```

以上makefile定义了`include`和`lib`目录的路径，并将对象文件`.o`放置在`src`目录中的`obj`子目录中。它还为您想要包含的任何库定义了一个宏，例如数学库`-lm`。此makefile应位于`src`目录中。

请注意，如果您键入`make clean`，它还包含一个清理源和对象目录的规则。`.PHONY`规则阻止`make`使用名为`clean`的文件。

