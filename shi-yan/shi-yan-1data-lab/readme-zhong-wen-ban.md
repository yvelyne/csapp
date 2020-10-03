# README（中文版）

> **CS:APP Data Lab**
>
> 给讲师的指导
>
> May 31, 2011：现在包含了“击败教授”竞赛
>
> Copyright \(c\) 2002-2018, R. Bryant and D. O'Hallaron

此目录包含运行 CS:APP Data Lab 所需的文件，它有助于培养学生对位表示、补码运算和 IEEE 浮点的理解。

为了好玩，我们还提供了一个新的基于 HTTP 的用户级“击败教授”竞赛，取代了旧的基于电子邮件的版本。新的比赛是完全独立的，不需要 root 密码。唯一的要求是在 Linux 机器上有一个具有 IP 地址的用户帐户。

系统需求：使用 bison 和 flex 构建 dlc。

## 1. 概述

在该实验中，学生处理一个名为 bits.c 的 C 文件，它由一系列编程“谜题” 组成。每个谜题都是一个需要完善的函数体，从而实现一个特定的数学函数，比如“绝对值”。在解决非浮点谜题时，学生仅能使用直线 C 代码和一组受限的 C 语言算术和逻辑运算符。对于浮点谜题，他们可以使用条件句和任意运算符。

学生使用以下三种工具检查作业。讲师使用相同的工具来给分。

1. **dlc：**一个“数据实验编译器”，用 bits.c 检查每个函数是否符合编码准则，检查学生是否使用少于最大数量的运算符，是否只使用直线代码，是否只使用合法运算符。其源代码和一个 Linux 二进制文件都包含在实验中。
2. **btest：**一个测试工具，用于检查 bits.c 中函数的正确性。这个工具已经得到了显著的改进，现在可以检查整数和浮点表示的大范围（wide swaths）边缘用例（edge cases），比如 0、最小有符号数（Tmin）、非正规数和正规数的边界（denorm-norm boundary） 和 无限大（inf）。
3. **driver.pl：**一个自动评分驱动程序，它使用 dlc 和 btest 来检查 bits.c 中每个测试函数的正确性，以及是否符合编码准则。

实验的默认版本包括 15 个谜题，位于 **./src/selections.c** 中，从目录 **./src/puzzles/** 中定义的 73 个标准谜题中选择。你可以从标准的谜题中选择一组不同的拼图来定制每个学期的实验。

你也可以自己定义新的谜题，并将它们添加到标准集合中。请参阅 **./src/README** 以获取如何向标准集合添加新谜题的说明。

注：如果你定义了新的谜题，请发送给我（Dave O'Hallaron, droh@cs.cmu.edu）这样我就可以将它们添加到 data lab 发行版的标准谜题集中。

## 2. 文件

所有的 CS:APP 实验都有着相同的简单的顶层目录结构：

| 文件名 | 说明 |
| :--- | :--- |
| Makefile | 构建整个实验。 |
| README | 本文件。 |
| src/ | 包含实验的所有源代码。 |
| datalab-handout/ | 发给学生的讲义目录。由 Makefile 从 ./src 中的文件生成。不要修改此目录中的任何内容。 |
| grade/ | 自动评分脚本，讲师可以用它来给学生提交的文件打分。 |
| writeup/ | LaTeX 实验报告样例。 |
| contest/ | 可选的“击败教授”比赛所需的所有文件。 |

## 3. 构建实验

**第 0 步。**如果打算运行“击败教授”（第 5 节）那么编辑 ./contest/Contest.pm 文件，以便驱动程序知道将结果发送到何处。参考 ./contest/README 获取简单的说明。如果您决定_不_参加比赛，那么在这一步中什么都不做。

**第 1 步。**编辑文件 **./src/selections.c** 选择要包含的谜题。默认的 **./src/selections.c** 来自 CMU 的 Data Lab 此前的一个实例。文件 **./src/selections-all.c** 包含可供选择的谜题的完整列表。

**第 2 步。**修改 **./writeup** 中 的 LaTeX 实验报告，定制成你的课程所需。

**第 3 步。**在当前目录中键入以下内容：

```bash
unix> make clean
unix> make
```

Makefile 生成 btest 源文件，构建 dlc 二进制文件（如果需要），格式化实验报告，然后将 btest、dlc 二进制文件和驱动程序复制到讲义目录。之后，它将构建讲义目录的 tar 文件（位于 **./datalab-handout.tar**），然后你可以将其发给学生。

关于二进制可移植性的注意事项：dlc 作为二进制文件放在 **datalab-handout** 目录中。由于动态库的不同版本，Linux 二进制文件并非总能跨发行版移植。需要注意的是，应在与学生所用机器兼容的一台机器上编译 dlc。

注意：运行 “make” 也会自动生成谜题的解答，可以在 **./src/bits.c** 和 **./src/bits.c-solution** 中找到。

## 4. 给实验评分






