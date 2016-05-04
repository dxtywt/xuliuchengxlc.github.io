---

yout: post
title: tmux备忘录
tags: tmux
author: Liucheng Xu
disqus: "y"
published: true

---

* TOC
{:toc}

### 适用场景

tmux是一个优秀的终端多路复用软件，类似GNU Screen，但来自于OpenBSD，采用BSD授权。使用它最直观的好处就是，通过一个终端登录远程主机并运行tmux后，在其中可以开启多个控制台而无需再“浪费”多余的终端来连接这台远程主机；当然其功能远不止于此，比如分屏(当然其他一些软甲也能达到这个目的，比如vim，但我还是喜欢tmux的分屏)。

![tmux](/images/blog/2016/04-01/screen.png)

为什么使用tmux： 

tmux比screen有更多的功能，能够保持工作环境的**连续性**。例如tmux解决如下的问题：

1. 下班后，如果你需要断开ssh或关闭电脑，你的ssh连接将丢失；

2. 在公司或者实验室打开的ssh，在其他地方也需要访问，比如宿舍或家里；

3. ssh可能由于一些原因中途意外断开(比如长时间没有操作)导致操作中断；

安装完成后输入命令tmux即可打开软件，界面十分简单，类似一个下方带有状态栏的终端控制台；但根据tmux的定义，在开启了tmux服务器后，会首先创建一个会话，而这个会话则会首先创建一个窗口，其中仅包含一个面板；也就是说，这里看到的所谓终端控制台应该称作tmux的一个面板，虽然其使用方法与终端控制台完全相同。

tmux使用C/S模型构建，主要包括以下单元模块：

- server服务器。输入tmux命令时就开启了一个服务器。

- session会话。一个服务器可以包含多个会话。

- window窗口。一个会话可以包含多个窗口。

- pane面板。一个窗口可以包含多个面板。

![tmux](/images/blog/2016/04-01/tmux.png)

**远程主机连接：**

- 一键启动远程主机上的 tmux：  
`ssh -t username@server.com tmux` 

- 如果你之前在远程主机上已经开启了 tmux 的话，用以下命令。
  
  远程主机仅有一个tmux会话，直接进行重连：  
  `ssh -t username@server.com tmux a`

  远程主机有多个tmux会话，我们想要指定重新连接名为foo的tmux会话：  
  `ssh -t username@server.com tmux a -t foo`

### 配置文件
最全面的文档当然是官方的manual page, [tmux.github.io](https://tmux.github.io/). 如果在网上搜索的话你会发现大多的tmux配置文件都是大同小异. 在我的配置文件并没有像大多配置一样将tmux的前缀键(类似emacs)的前缀键重映射为`Ctrl+a`，而是选择了默认设置`Ctrl+b`. 另外在颜色选择上不同平台下渲染的效果不一样, 注意适应。

下面是我的配置文件. 

<script src="https://gist.github.com/xuliuchengxlc/bae72ae083aecdbf2ee8bfba81401908.js"></script>





### Getting Started

开始tmux使用。以下大部分内容均为默认设置, 如果在配置文件修改了设置则以配置文件为准。**且在英文输入状态下进行。**

推荐材料 [tmux:Productive Mouse-Free Deveplement 中文版](http://www.kancloud.cn/kancloud/tmux/62459)

commend | explanation
:---:|:---:
`tmux` | 启动tmux会话
`tmux new -s myname` | 创建一个名为myname的新的会话
`tmux a` / `tmux at` / `tmux attach` | 如果当前仅有一个会话，重新连接该会话
`tmux a -t myname` | 连接到指定会话myname
`tmux ls` | 显示所有会话
`tmux kill-session -t myname` | 关闭指定会话myname


### Sessions

以下的session(会话)、window(窗口)与pane(面板)命令中，PREFIX表示前缀键, 即如果未重映射前缀键的话，PREFIX表示`Ctrl+b`，然后再按后面的键。

会话命令加前缀键。比如下面的s即指prefix+s，Ctrl+b+s.

commend | explanation
:---:|:---:
`:new<CR>` | New session
`d (detach)` | 从一个会话中分离，让该会话在后台运行
`$` | 重命名会话
`s` | 显示会话
`(` | 切换到上一会话
`)` | 切换到下一会话
`L (Last)` | 切换到最后一个会话

### Windows(Tabs)

窗口操作。加前缀键。

commend | explanation
:---:|:---:
`c (create)` | 创建新窗口
`w (window)` | 显示窗口列表
`f (find)` | 查找窗口
`,` | 重命名窗口
`&` | 关闭当前窗口，带有确认提示
`n (next)` | 切换到下一窗口
`p (previous)` | 切换到上一窗口
`l (last)` | 切换到最后一个使用的窗口

### Panes (Splits)

面板操作。加前缀键。

commend | explanation
:---:|:---:
`%` | 垂直分割面板 (默认)
`|` | 垂直分割面板 (配置修改后) In tmux.conf: bind-key split-window -v
`"` | 水平分割面板 (默认)
`-` | 水平分割面板 (配置修改后) In tmux.conf: bind-key split-window -h
`o` | 在已打开的面板间循环移动当前焦点
`q` | 短暂显示面板编号
`x` | 关闭当前面板，带有确认提示
`z` | Toggle active pane between zoomed and unzoomed
`+` | Break pane into window (e.g. to select text by mouse to copy)
`-` | Restore pane from window
`Space` | 循环使用tmux的几个默认面板布局
`Q` | Show pane numbers When the numbers show up type the key to go to that pane
`{` | 移动当前面板到左侧
`}` | 移动当前面板到右侧

### Copy Mode

Pressing PREFIX-[ places us in Copy mode. We can then use our movement keys to move our cursor around the screen. By default, the arrow keys work. We set our configuration file to use Vim keys for moving between windows and resizing panes so we wouldn’t have to take our hands off the home row. tmux has a vi mode for working with the buffer as well. To enable it, add this line to .tmux.conf:

`setw -g mode-keys vi`

With this option set, we can use `h`, `j`, `k`, and `l` to move around our buffer.

To get out of Copy mode, we just press the Enter key. Moving around one character at a time isn’t very efficient. Since we enabled vi mode, we can also use some other visible shortcuts to move around the buffer.

For example, we can use w to jump to the next word and b to jump back one word. And we can use f, followed by any character, to jump to that character on the same line, and F to jump backwards on the line.

commend | explanation
:---:|:---:
`^` | Back to indentation
`Esc` | Clear selection
`Enter` | Copy selection
`j` | Cursor down
`h`| Cursor left
`l` | Cursor right
`L` | Cursor to bottom line
`M` | Cursor to middle line
`H` | Cursor to top line
`k` | Cursor up
`d` | Delete entire line
`D` | Delete to end of line
`$` | End of line
`:` | Goto line
`C-d` | Half page down
`C-u` | Half page up
`C-f` | Next page
`w` | Next word
`p` | Paste buffer
`C-b` | Previous page
`b` | Previous word
`q` | Quit mode
`C-Down` / `J` | Scroll down
`C-Up` / `K`   | Scroll up
`n` | Search again 
`?` | Search backward
`/` | Search forward
`0` | Start of line
`Space` | Start selection

