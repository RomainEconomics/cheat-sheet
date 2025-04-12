# Tmux commands reference guide

## introduction

Tmux (terminal multiplexer) is a powerful tool that allows you to create multiple terminal sessions within a single window. this guide covers the essential tmux commands to help you navigate and use tmux effectively.

## basic concepts

- **session**: a collection of windows (can be detached and reattached)
- **window**: like a tab in your terminal (contains one or more panes)
- **pane**: a split section of a window running a separate shell

## starting and managing sessions

### starting tmux

```bash
tmux                     # start a new session
tmux new -s sessionname  # start a new session with a name
```

### session management

```bash
tmux ls                  # list all sessions
tmux attach              # attach to the last session
tmux attach -t name      # attach to a specific session
tmux kill-session -t name # kill a specific session
tmux rename-session -t old new # rename a session
```

## prefix key

most tmux commands are executed by first pressing the prefix key combination (default: `ctrl+b`), followed by another key.

## window management

```
prefix + c               # create a new window
prefix + ,               # rename current window
prefix + n               # move to next window
prefix + p               # move to previous window
prefix + number          # switch to window by number (0-9)
prefix + w               # list all windows
prefix + &               # kill current window (with confirmation)
prefix + f               # find window by name
```

## pane management

```
prefix + "               # split pane horizontally
prefix + %               # split pane vertically
prefix + arrow key       # switch to pane in that direction
prefix + o               # cycle through panes
prefix + q               # show pane numbers (press number to select)
prefix + x               # kill current pane (with confirmation)
prefix + z               # toggle pane zoom (maximize/restore pane)
prefix + {               # move current pane left
prefix + }               # move current pane right
prefix + ctrl+arrow      # resize pane in that direction
prefix + space           # cycle through pane layouts
```

## copy mode (vi-like navigation)

```
prefix + [               # enter copy mode
q                        # exit copy mode
space                    # start selection (in copy mode)
enter                    # copy selection (in copy mode)
prefix + ]               # paste copied text
```

## other useful commands

```
prefix + d               # detach from session
prefix + t               # show clock
prefix + :               # enter command mode
prefix + ?               # show key bindings
```

## command mode commands

after pressing `prefix + :`, you can enter these commands:

```
new-session -s name      # create new session
set -g mouse on          # enable mouse support
set-window-option -g mode-keys vi  # use vi keys in copy mode
source-file ~/.tmux.conf # reload configuration
```

## configuration

tmux can be customized by editing the `~/.tmux.conf` file. common customizations include:

- changing the prefix key
- enabling mouse support
- customizing status bar
- setting different key bindings

## advanced features

### session management

```
tmux new-session -d -s name "command"  # start a detached session running a command
```

### window and pane synchronization

```
:setw synchronize-panes on  # type the same commands in all panes
:setw synchronize-panes off # turn off synchronization
```

## tips for beginners

1. start with basic window and pane management
2. learn to detach and reattach to sessions
3. create a custom `.tmux.conf` file as you become more comfortable
4. use tmux cheat sheets until commands become muscle memory
