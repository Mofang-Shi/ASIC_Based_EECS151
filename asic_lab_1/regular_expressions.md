# 正则表达式教程

## 介绍

本教程来自`UCB EECS151 ASIC Lab1`推荐阅读的教程：[Learn Regular Expressions with simple, interactive exercises.](https://regexone.com)

## Lesson 1: 简介

正则表达式（Regular expressions）在从代码、日志文件、电子表格甚至文档（ code, log files, spreadsheets, or even documents）等文本中提取信息方面非常有用。虽然形式语言（formal languages）背后有很多理论，但本课程和示例将探索正则表达式的更实际用途，以便可以尽快使用它们。

使用正则表达式时要识别的第一件事是，**一切本质上都是字符（ everything is essentially a character）**，我们正在编写模式来匹配特定的字符序列（sequence of characters，也称为字符串，string）。大多数模式使用普通的`ASCII`，其中包括字母、数字、标点符号（letters, digits, punctuation）和键盘上的其他符号，如%#$@!，但`Unicode字符`也可用于匹配任何类型的国际文本。

请注意以下图片中键入字符时是如何匹配的：

![正确](fig/regular_expressions_lesson1_fig_1.png "regular_expressions")

![正确](fig/regular_expressions_lesson1_fig_2.png "regular_expressions")

![错误](fig/regular_expressions_lesson1_fig_3.png "regular_expressions")

## Lesson 1½: 数字（digits）

字符包括普通字母（normal letters），但也包括数字（digits）。事实上，数字0-9也只是字符，如果您查看`ASCII表`，它们会按一定的顺序列出。

在本课程中，您将了解一些用于正则表达式的**特殊元字符（metacharacters）**，这些元字符可用于匹配特定类型的字符。

字符`\d`可以代替从0到9的任何一个数字。前面的斜杠将其与简单的d字符区分开来，并表示它是一个元字符。

与之对应的，`\D`可以代替非数字的任何一个字符。

注意下图的模式如何匹配字符串中的任何地方，**而不仅仅是从第一个字符开始：**

![正确](fig/regular_expressions_lesson1_5_fig_4.png "regular_expressions")

## Lesson 2: 点（`.`dot）

我们经常使用正则表达式匹配不知道确切内容的文本，但它们具有共同的模式或结构（pattern or structure），例如电话号码或邮政编码。

通配符（wildcard）由`.`元字符（metacharacter）表示，可以匹配任何单个字符（字母、数字、空格、所有内容）。

您可能会注意到，这实际上覆盖了句号字符的匹配，因此为了具体匹配句点，您需要使用斜杠（slash）`\.`相应地转义点（escape the dot）。

下图是几个字符不同但长度相同的字符串，要匹配前三个字符串必须转义点元字符以匹配某些行中的点：

![正确](fig/regular_expressions_lesson2_fig_1.png "regular_expressions")

## Lesson 3: 匹配特定字符（Matching specific characters）

有一种方法可以使用正则表达式匹配特定字符，方法是在方括号内定义它们。

例如，`[abc]`将只匹配单个a、b或c字母，而不会匹配其他字母。

![正确](fig/regular_expressions_lesson3_fig_1.png "regular_expressions")

## Lesson 4: 排除特定字符（Excluding specific characters）

使用方括号`[]`和`^`（hat）排除特定字符。

例如，`[^abc]`将匹配除字母a、b或c以外的任何单个字符。

请注意，这种类型的大多数图案也可以用上一课中的技术来书写，可以在编写自己的模式时决定哪一个更容易编写和理解。

![正确](fig/regular_expressions_lesson4_fig_1.png "regular_expressions")

![正确](fig/regular_expressions_lesson4_fig_2.png "regular_expressions")

## Lesson 5: 字符范围（Character ranges）

如果我们想匹配一个可以处于顺序范围字符的字符呢？

幸运的是，在使用方括号`[]`表示法时，通过使用破折号`-`来指示字符范围来匹配顺序字符列表中的字符。

例如，`[0-6]`只会匹配从零到六的任何一位数字字符，而不会匹配其他字符。

同样，`[^n-p]`只会匹配除了字母n到p外任何单个字符。

同一组括号中也可以与单个字符一起使用多个字符范围。这方面的一个例子是字母数字`\w`元字符，它等同于字符范围`[A-Za-z0-9_]`，通常用于匹配英语文本中的字符。

![正确](fig/regular_expressions_lesson5_fig_1.png "regular_expressions")

## Lesson 6: 重复匹配（Catching some zzz'）

**注意：并非所有正则表达式实现都支持以下重复语法的某些部分。**

到目前为止，我们已经学会了如何指定我们想要匹配的字符范围，但我们想要匹配的字符的重复次数如何？我们可以做到这一点的一种方法是使用大括号表示法`{}`指定每个字符的重复次数。

例如，`a{3}`将恰好匹配一个字符三次。某些正则表达式引擎甚至允许您为这种重复指定一个范围，例如，`a{1,3}`将匹配字符不超过3次，但不少于1次。

此数量`{n}`可以与任何字符或特殊元字符一起使用，例如`w{3}`（3个w），`[wxy]{5}`（五个字符，每个字符可以是w、x或y）和`.{2,6}`（任2-6个任意字符）。

![正确](fig/regular_expressions_lesson6_fig_1.png "regular_expressions")

## 第7课：匹配任意数量（Mr. Kleene, Mr. Kleene）

正则表达式中一个强大的概念是匹配任意数量的字符的能力。

例如，有两个数字：`$25,000`和`$25`

为了匹配上述数字，我们可以使用`\d*`来匹配任意数量的位数，但更严格的正则表达式是`\d+`，这可以确保输入字符串至少有一位数字。

这些量词可以与任何字符或特殊元字符一起使用，例如`a+`（一个或多个a）、`[abc]+`（任何a、b或c字符的一个或多个）和`.*`（没有字符或者有任意数量的任意字符）。

![正确](fig/regular_expressions_lesson7_fig_1.png "regular_expressions")

![正确](fig/regular_expressions_lesson7_fig_2.png "regular_expressions")
