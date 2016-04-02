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
下面是我的配置文件, 在网上搜索而来，如有更新，可以再这里找到[tmux config](https://github.com/xuliuchengxlc/dotfiles/blob/master/tmux/.tmux.conf). 不过最好的选择当然是官方的manual page, [tmux.github.io](https://tmux.github.io/). 如果在网上搜索的话你会发现大多的tmux配置文件都是大同小异. 在我的配置文件并没有像大多配置一样将tmux的前缀键(类似emacs)的前缀键重映射为`Ctrl+a`，而是选择了默认设置`Ctrl+b`. 另外在颜色选择上不同平台下渲染的效果不一样, 注意适应。

```
# 设置终端类型为256色
set -g default-terminal "screen-256color"

# 事件窗口信息，如有内容变动，进行提示
setw -g monitor-activity on
set -g visual-activity on
set -g status-utf8 on
set -g history-limit 100000    #  scrollback buffer n lines
set -g mode-keys vi    #  user vi mode

# 支持鼠标选择窗口，调节窗口大小
setw -g mode-mouse on
set -g mouse-select-pane on
set -g mouse-resize-pane on
set -g mouse-select-window on

# 重新绑定纵向和横向切分window快捷键。|，-，更直观地表明了切割方向
bind | split-window -h
bind - split-window -v

# 在不同面板间切换，改为vim风格
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# tmux有一个延时以方便用户按键组合，默认有点长。这里设置为1秒钟
set -s escape-time 1

# 设置动态加载tmux配置文件的快捷键
bind r source-file ~/.tmux.conf \; display "Configuration Reloaded"

# 设置窗口标签的前景及背景色
setw -g window-status-fg colour190
setw -g window-status-bg default 
setw -g window-status-attr dim

# 设置当前窗口标签的前景及背景色,所谓当前窗口标签会显示在状态栏中间
setw -g window-status-current-fg colour255
setw -g window-status-current-bg colour130
setw -g window-status-current-attr bright

# 设置窗口分割的边框颜色
set -g pane-border-fg colour189
set -g pane-border-bg black

# 设置当前窗口分割的边框颜色
set -g pane-active-border-fg white
set -g pane-active-border-bg colour208

# 设置提示信息的前景及背景色
set -g message-fg colour232
set -g message-bg colour23
set -g message-attr bright

#set -g set-titles-string '#T'

###################  状态栏设置  ###############################
# 以下色彩为mac环境下，Linux下可能需重新设置颜色
# 设置状态栏前景色，背景色
#set -g status-fg white
#set -g status-bg black

# 设置状态栏前景及背景色
set -g status-bg colour23
set -g status-fg colour238

# 设置状态栏左部宽度  默认为10
set -g status-left-length 40
# 设置状态栏左部显示内容。
set -g status-left "#[fg=magenta,bold]session #S:
#[fg=yellow]window #I:#[fg=cyan]pane #P#[default]"
# 设置状态栏右部宽度
set -g status-right-length 80
# 设置状态栏右部内容，这里设置为时间信息
set -g status-right "#[fg=cyan]%d%b,%R"
# 窗口信息居中显示
set -g status-justify centre
# 设置状态栏更新时间 每60秒更新一次，默认是15秒更新
set -g status-interval 60
```



### Getting Started

开始tmux使用。以下所有内容均为默认设置, 如果在配置文件修改了设置则以配置文件为准。

commend | explanation
:---:|:---:
`tmux` | start new 
`tmux new -s myname` | start new session with name myname
`tmux a` / `tmux at` / `tmux attach` | Attach
`tmux a -t myname` | Attach to named
`tmux ls` | list sessions
`tmux kill-session -t myname` | kill session


### Sessions

以下的session(会话)、window(窗口)与pane(面板)命令中，PREFIX表示前缀键, 即如果未重映射前缀键的话，PREFIX表示`Ctrl+b`，然后再按后面的键。

commend | explanation
:---:|:---:
`PREFIX-:new<CR>` | New session
`PREFIX-$` | Name session
`PREFIX-s` | List sessions
`PREFIX-(` | Previous session
`PREFIX-)` | Next session
`PREFIX-L` | Last session

### Windows(Tabs)

窗口操作。

commend | explanation
:---:|:---:
`PREFIX-c` | New window
`REFIX-w` | List windows
`PREFIX-f` | Find window
`PREFIX-,` | Name window
`PREFIX-&` | Kill window
`PREFIX-n` | Next window
`PREFIX-p` | Previous window
`PREFIX-l` | Previously selected window

### Panes (Splits)

面板操作。

commend | explanation
:---:|:---:
`PREFIX-%` | Vertical split (Standard)
`PREFIX-|` | Vertical split (Personal) In tmux.conf: bind-key split-window -v
`PREFIX-"` | Horizontal split (Standard)
`PREFIX- -` | Horizontal split (Personal) In tmux.conf: bind-key split-window -h
`PREFIX-o` | Switch focus between panes
`PREFIX-q` | Show pane numbers
`PREFIX-x` | Kill pane
`PREFIX-z` | Toggle active pane between zoomed and unzoomed
`PREFIX-"+"` | Break pane into window (e.g. to select text by mouse to copy)
`PREFIX-"-"` | Restore pane from window
`PREFIX-Space` | Toggle between layouts
`PREFIX-Q` | Show pane numbers When the numbers show up type the key to go to that pane
`PREFIX-{` | Move the current pane left
`PREFIX-}` | Move the current pane right

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

