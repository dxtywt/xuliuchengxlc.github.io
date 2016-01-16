---
layout: post
title: 我的Windows环境 ---- 漂亮，简单，实用
disqus: y
---

工欲善其事，必先利其器。作为一个IT人，可能每天面对的最多的就是我们的电脑了，那么一个可心的操作环境显然必不可少。不仅仅是为了心情愉悦，同时也是为了提高工作效率。

目前我一般使用两台电脑：台式机加上一台Retina MacBook pro。台式机主要是屏幕大，配置高，什么时候不满意了还可以自主升级配置，而mac自然是类unix系统和视网膜屏幕让我爱不释手。虽然mac很漂亮，但win才是我的主力机。即使Windows没有os x外表那么华丽，但是经过一番努力还是能够提升它的颜值与实用性的。

这里可能并不会做很多详细的介绍，有心的人自然会去搜索，去试用，去了解。我只是将我的一些经验之谈分享出来供大家参考。

下面就来介绍一下我的Windows环境配置，操作系统为Windows 10 64位.

##提高效率

####Everything

**快速检索文件**

相信很多人都知道everything，当我们需要找到某个文件时非它莫属，功能十分强大。
搜索几乎是秒出结果，堪比mac下的spotlight，而且支持正则表达式搜索。

####Executor

**自定义快捷键**,快速启动程序。

虽然知道这个软件是因为它能够像mac下面的Alfred能够快速唤出程序，但是因为这个功能体验并不好，实际我用的最多的是它的自定义快捷键功能。

executor的keywords设置很简单，在setting里面Add Keywords就可以设置相关快捷键。
我的一些快捷键设置如下：

| 快捷键 | 软件 |
|--------|--------|
|  <code>ctrl</code> + 1      | chrome:       |
|  <code>ctrl</code> + 2      | Firefox:       |
|  <code>ctrl</code> + 4      | 欧路词典 or 有道词典   |
|  <code>ctrl</code> + 5      | 福昕阅读器       |
|  <code>ctrl</code> + 7      | :SumatraPDF       |
|  <code>ctrl</code> + 0      | :everything       |

记忆起来也很简单，everything最常用就用<code>ctrl</code>+0，<code>ctrl</code>辅以1,2为常用的两个浏览器，4、5、7分别于对应的软件名字数。

另外关于everything的快捷键设置有些不同，不能勾选only one instance running选项，否则快捷键无效。

####QTTabBar

**增强文件资源管理器**

与QTTabBar类似的还有一个非常好的软件clover，可惜在win10下面的表现实在是糟糕，频繁崩溃。

####SumatraPDF

**用类似vim的方式阅读pdf**，可以实现全键盘操作。

####VistaSwitcher

**简化任务切换窗口**

虽然win10的任务切换也还不错，但是窗口开多了以后实在是显得有些眼花缭乱。

虽然VistaSwitcher也是许久没有更新，不过在win10的表现除了一点小瑕疵，还算不错，很稳定。

- 注意一下外观设置：
	- 不要启用Aero blur效果，否则背景会很黑且不通透，显得很难看；
	- 显示任务编号

##提升颜值

####StartIsBack

**美化任务栏**

[这里是分享的免注册版本，直接安装即可。在分享的链接中还有其他软件，不过还是大家尽可能的自行下载最新可用版本获得更好的体验](http://pan.baidu.com/s/1jHoTxGi) 密码: n7nj

win10的任务栏实在是不好看，黑色的一条杠横在那儿。用了startisback以后可以将任务栏设置为透明状态，并且还可以设置开始菜单。
可能安装以后有人会找不到程序在哪里，用上面的everything搜索startisback就会发现StartIsBackCfg.exe,运行它就会进入到设置页面。

- 主要是设置任务栏的透明度。
	- **自定义任务栏颜色**改变透明度
	- 选择**使用较大的任务栏图标**。

####NetSpeedMonitor

**在任务栏显示网速**

用这个软件主要是想关闭什么管家、杀毒之类的加速球，嫌它碍事。台式机有32G内存，所以一般不用担心内存占用的问题。实在有需要的时候，<code>Ctrl</code>+<code>shift</code>+<code>ESC</code>调出资源管理器也就是了。因此只用看看网速就安心了。

####MacType

**美化Windows字体**

使用前后的确视觉感受有明显区别，很多软件都有不错的效果。不过也有没办法通过MacType渲染的软件，比如chrome。
我采用的是默认的**LCD**效果，选择以注册表方式加载。



