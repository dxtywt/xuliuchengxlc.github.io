---
layout: post
title: 教你LaTeX快速入门
tags: LaTeX
disqus: y
---

* TOC
{:toc}

对于理工科的学生来说，尤其是从研究生阶段开始，LaTeX应该会是日常中必不可少的科研工具。目前我并不是一个LaTeX高手，但至少应该算是已经入门LaTeX。所谓入门的要求至少应该是能够完成一些日常写作的要求，比如写个report什么的，遇到一些常见的问题能够Google并解决。

此篇为写给一些想快速入门LaTeX的朋友,本人学识与能力有限，以下内容如有纰漏或错误，欢迎来信。

---

## LaTeX概览

摘自维基百科：  

>LaTeX, 是一种基于TEX的排版系统，由美国电脑学家莱斯利·兰伯特在20世纪80年代初期开发，利用这种格式，即使用户没有排版和程序设计的知识也可以充分发挥由TEX所提供的强大功能，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。这个系统同样适用于生成从简单的信件到完整书籍的所有其他种类的文档。

简单点说：LaTeX基于TeX，目的主要是为了方便排版。在学术界的论文，尤其是数学、计算机等学科论文都是由LaTeX编写。

我的一点理解：
在稍微了解一点LaTeX后，你会发现LaTeX的工作方式类似HTML，都是由源文件（.tex or .html）经由引擎（TeX or browser）渲染产生最终效果（得到PDF文件 或者 生成页面）。两者极其神似，包括语法规则与工作方式。所以呢，与HTML一样，LaTeX其实很简单，不过是调整样式等可能会很麻烦，因为会涉及到很多内容。

## 安装配置LaTeX

LaTeX配置环境很简单，只需2步即可：

1. 根据平台选择一个TeX发行版进行安装,建议选择最全功能最多的版本。TeX发行版的概念相当于Linux及其发行版，Linux内核虽然只有一个，但是有很多基于内核的不同特色的Linux发行版，Ubuntu，Fedora等等不胜枚举。

    - TeXLive for three platforms
    
        [TeXLive](https://www.tug.org/texlive/)
    - Windows
    
        [CTeX套装](http://www.ctex.org/CTeXDownload)
    - Mac
    
        [MacTeX](http://tug.org/mactex/)

2. 选择一个合适的LaTeX编辑器。

	在安装好LaTeX环境以后，通常都会有一个自带的编辑器，比如CTex的WinEdt, Mac下的TeXShop, 不过功能并不强大，就好比Windows记事本，只有一些基本的文本编辑功能。
	
	在这里推荐一个我目前觉得还不错的LaTeX编辑器：**TeXstudio**。我试过WinEdt，TeXnicle，不过都比不上TeXstudio。

## 开始第一个LaTeX文档

打开TeXstudio，新建一个TeX文件，写入以下内容：

``` tex
 \documentclass{article}
 \begin{document}
 Here comes \LaTeX!
 \end{document}
```

点击 <code>F5</code>（默认快捷键）compile and view,即可看到效果。
![TeXstudio](/images/blog/2016/01-30/screen.png)

至此，一个极简易的LaTeX文档已经完成。以后的内容不过是多用多查，熟能生巧。  
记得找本LaTeX的书籍看一下，一来对于更为精细的知识做一个了解，二来可以作为工具书有问题的时候查询。我经常查的是 <<LaTeX入门与提高 第二版>>。

### LaTeX数学公式

学习LaTeX的一大初衷其实是为了书写数学公式。  
数学公式的练习始于markdown，因为很多markdown编辑器是支持LaTeX数学公式的，比如haroopad。那么不仅可以写出漂亮的公式，还能方便做笔记。

以下内容直接在支持数学公式的markdown编辑器中即可操作，而且是即时显示效果，对新手很有帮助。如果使用haroopad编辑器，请在**偏好设置**中**启用数学表达式**。

**学会书写LaTeX数学公式，只需要了解4个概念：**

1. 数学公式环境。
   LaTeX 的数学模式有两种：行内模式(inline)和行间模式(display)。前者在正文的行文中，插入数学公式；后者独立排列单独成行。

    在行文中，使用<code>$ ... $</code>可以插入行内公式，使用<code>\[ ... \]</code>可以插入行间公式，如果需要对行间公式进行编号，可以使用equation环境：

    ``` 
    \begin{equation}
    …
    \end{equation}
    ```
    
    行内公式也可以使用<code>\(...\)</code>来插入，略嫌麻烦。无编号的行间公式也可以使用<code>$$ ... $$</code>来插入，但是这样做会改变行文的默认行间距，不推荐。

    如果在markdown中使用LaTeX数学公式，我习惯用下面两种方式：
	    
	  - 行间公式  
	      <code>$$ 行间公式 $$</code>
	    
	  - 行内公式  
	      <code>$ 行内公式 $</code>

2. 凡是键盘不方便或者不能够表示的符号皆有命令，类似转义，讲究一点呢就叫做**控制序列**。比如求和符号$\sum$对应的命令为 <code>\sum</code>.

3. 上下标。<code>_{...}</code>表示下标，<code>^{...}</code>表示上标。它默认只作用于之后的一个字符，如果想对连续的几个字符起作用，请将这些字符用花括号{}括起来, 也就是下面分组的概念。

4. 分组。很简单，就是用<code>{...}</code>将内容包含起来视作整体，比如上下标很长的时候。遇到什么时候得到的效果不是预期，那么很可能你需要加个分组，也就是添个大括号<code>{...}</code>.

| LaTeX命令 | 预览效果 |
|:--------:|:--------:|
|  <code>$ x_i $</code>      |  $x_i$      |
|<code>$ x^2 $</code>|$x^2$|
|<code>$ x^ {y^z} $</code>|$x^{y^z}$|
|<code>$ \int_a^b f(x)$</code>|$\int_a^bf(x)$|
|<code>$ \frac ab $</code>|$\frac ab$|

有了这几个概念以后，再动手写几个就大概懂了。无论多么复杂的公式都是有一个个简单的东西构成。

### LaTeX中文支持

不同环境具体操作有所不同，下面介绍Windows与Mac平台。

- Windows  
Windows平台比较简单，引入CJK宏包并应用CJK环境即可。    

LaTeX将 

``` tex
\begin{...}
   content
\end{...}
```

称为<code>...</code>环境。在对应环境中 content 产生对应效果。
![winedt](/images/blog/2016/01-30/winedt.png)

- Mac  
系统为osx 10.11.3, Mac添加中文支持稍微多几个操作，除了引入xeCJK宏包，还要设置字体名称。  
关于设置字体名称，spotlight输入 zitice 打开 mac 的字体册,从字体中选择一个，将其名称填入，如华文楷体的名称为 STKaiti 。  
如果没有显示字体名称，请 <code>command+I</code> 或在显示-->显示字体信息即可。
![font](/images/blog/2016/01-30/font.png)
![macchinese](/images/blog/2016/01-30/MacChinese.png)

### 几个LaTeX推荐网站

- [Detexify LaTeX handwritten symbol recognition](http://detexify.kirelabs.org/classify.html).

	通过手写识别LaTeX符号，识别率很高。
	尤其是当看到一个符号却不知道其LaTeX命令的时候它很有用。只要画出记忆中符号的样子，就会自动出现各种可能想要的表示方法。
    
- [LaTeX公式编辑器](http://zh.numberempire.com/texequationeditor/equationeditor.php)

	对于书写LaTeX公式提供一点便利。
	
- [在线LaTeX编辑器shareLaTeX](https://cn.sharelatex.com/)

  好处就是不用本地搭建环境，直接在线操作。还有很多LaTeX模板可供选择。
