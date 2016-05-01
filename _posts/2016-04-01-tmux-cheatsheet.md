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
`d` | 从一个会话中分离，让该会话在后台运行
`$` | 重命名会话
`s` | 显示会话
`(` | 切换到上一会话
`)` | 切换到下一会话
`L` | 切换到最后一个会话

### Windows(Tabs)

窗口操作。加前缀键。

commend | explanation
:---:|:---:
`c` | 创建新窗口
`w` | 显示窗口列表
`f` | 查找窗口
`,` | 重命名窗口
`&` | 关闭当前窗口，带有确认提示
`n` | 切换到下一窗口
`p` | 切换到上一窗口
`l` | 切换到最后一个使用的窗口

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

