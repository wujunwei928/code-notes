
https://www.gnu.org/ 
https://www.emacswiki.org/  
http://emacs.sexy/  
http://planet.emacsen.org/  

http://man.openbsd.org/OpenBSD-current/man1/tmux 

[EmacsWiki: Moving The Ctrl Key](https://www.emacswiki.org/emacs/MovingTheCtrlKey#toc13)  
[tmux：打造精致与实用并存的终端](https://segmentfault.com/a/1190000008188987)  
[初始化TMUX工作区](http://harttle.com/2016/09/23/tmux-workspace-setup.html)  
[优雅地使用命令行：Tmux 终端复用](http://harttle.com/2015/11/06/tmux-startup.html)  


[fzf + vim + tmux](https://junegunn.kr/2014/04/fzf+vim+tmux/)  

**tmux简明配置**
```bash

# use C-a, since it's on the home row and easier to hit than C-b
set-option -g prefix C-a
unbind-key C-a
bind-key C-a send-prefix

# 窗口从 1 开始计数, 默认从 0 开始
set -g base-index 1

# 重新加载tmux配置文件
bind-key r source-file ~/.tmux.conf \; display-message "tmux.conf reloaded."

# vi is good
setw -g mode-keys vi

# mouse behavior
# set -g mouse on

# 新打开 window 或 pane 的时候, 定位到当前所在文件夹
bind '"' split-window -c '#{pane_current_path}'
bind '%' split-window -h -c '#{pane_current_path}'

# 使用vi鍵盤選擇pane
bind-key h select-pane -L
bind-key j select-pane -D
bind-key k select-pane -U
bind-key l select-pane -R

# Setup 'v' to begin selection as in Vim
bind-key -t vi-copy v begin-selection
bind-key -t vi-copy y copy-pipe "reattach-to-user-namespace pbcopy"

# Update default binding of `Enter` to also use copy-pipe
unbind -t vi-copy Enter
bind-key -t vi-copy Enter copy-pipe "reattach-to-user-namespace pbcopy"

set-window-option -g display-panes-time 1500

# # Status Bar
# set-option -g status-interval 1
# set-option -g status-left ''
# set-option -g status-right '%l:%M%p'
# set-window-option -g window-status-current-fg magenta
# set-option -g status-fg default

# # Status Bar solarized-dark (default)
# set-option -g status-bg black
# set-option -g pane-active-border-fg black
# set-option -g pane-border-fg black

# # Status Bar solarized-light
# if-shell "[ \"$COLORFGBG\" = \"11;15\" ]" "set-option -g status-bg white"
# if-shell "[ \"$COLORFGBG\" = \"11;15\" ]" "set-option -g pane-active-border-fg white"
# if-shell "[ \"$COLORFGBG\" = \"11;15\" ]" "set-option -g pane-border-fg white"

# Set window notifications
setw -g monitor-activity on
set -g visual-activity on

# Enable native Mac OS X copy/paste
set-option -g default-command "/bin/bash -c 'which reattach-to-user-namespace >/dev/null && exec reattach-to-user-namespace $SHELL -l || exec $SHELL -l'"

# Allow the arrow key to be used immediately after changing windows
set-option -g repeat-time 0

# Fix to allow mousewheel/trackpad scrolling in tmux 2.1
bind-key -T root WheelUpPane if-shell -F -t = "#{alternate_on}" "send-keys -M" "select-pane -t =; copy-mode -e; send-keys -M"
bind-key -T root WheelDownPane if-shell -F -t = "#{alternate_on}" "send-keys -M" "select-pane -t =; send-keys -M"

# Disable assume-paste-time, so that iTerm2's "Send Hex Codes" feature works
# with tmux 2.1. This is backwards-compatible with earlier versions of tmux,
# AFAICT.
set-option -g assume-paste-time 0





```
