---

layout: post
title: "一种DEBUG_CATCH的简单用法"
description: "一种DEBUG_CATCH的简单用法"
category: Development
tags: [C++]
---
{% include JB/setup %}

我们编码过程中，常常需要在逻辑较复杂的代码中添加DEBUG_TRY和DEBUG_CATCH来进行异常捕获和记录异常信息。而我们使用DEBUG_CATCH时，90%以上的情况下，只是将出错的函数名打印出来，机械的复制函数名既繁琐无趣又容易出错，那么有没有简单的方法让DEBUG_CATCH替我们直接把出错函数打印出来呢？
答案当然是肯定的。要解决这个问题，就要用到编译器提供的 *FUNCTION*

大家都知道编译器有提供_*FILE和LINE用来打印当前代码的文件和行号，而在最新的ISO C标准中，如大家所知的C99，加入了另一个有用的、类似宏的表达式func，其会报告未修饰过的（也就是未裁剪过的）、正在被访问的函数名。请注意，func*_不是一个宏，因为预处理器对此函数一无所知；相反，它是作为一个隐式声明的常量字符数组实现的：

pre.
static const char *func*[] = "function-name";

官方C99标准为此目的定义的_*func标识符，确实值得大家关注，然而，ISO C++却不完全支持所有的C99扩展，因此，大多数的编译器提供商都使用FUNCTION*_ 取而代之，而 *FUNCTION* 通常是一个定义为 *func* 的宏，之所以使用这个名字，是因为它已受到了大多数的广泛支持。

在VS 2008中也提供了*FUCTION* 供我们使用。

有了*FUNCTION*，我们就能够很方便的调用DEBUG_CATCH(*FUNCTION*)来打印异常函数的名称了

pre.
DEBUG_TRY
//your code here
DEBUG_CATCH(*FUNCTION*)

或者除了函数名，你还想补充点什么：

pre.
DEBUG_CATCH("your words before"*FUNCTION*"your words after")

或者你觉得我只想打印函数名，又觉得写DEBUG_CATCH(*FUNCTION*)还是太麻烦了。我们可以定义一个无参的DEBUG_CATCH

pre.

#ifndef _DEBUG
#define DEBUG_CATCH0 DEBUG_CATCH(*FUNCTION*)
#else
#define DEBUG_CATCH0 }
#endif

这样，你就只要简单的像这样使用就可以了

pre.
DEBUG_TRY
//your code here
DEBUG_CATCH0
