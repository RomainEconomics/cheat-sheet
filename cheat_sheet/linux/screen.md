# Screen

Screen or GNU Screen is a terminal multiplexer. In other words, it means that you can start a screen session and then open any number of windows (virtual terminals). This does not contain **all** of screen's commands and options, read [GNU's manual](https://www.gnu.org/software/screen/manual/screen.html#Commands) to see everything

### Basics

| Command          | Description                                           |
| ---------------- | ----------------------------------------------------- |
| screen -S `name` | Start a named session                                 |
| ctrl+a ctrl+d    | Detach the current screen and go back to the terminal |
| screen -r `name` | Reattach to a screen (optionally by name)             |
| screen -ls       | List all sessions                                     |
| screen -list     | List all sessions                                     |
| ctrl+a c         | Create a new screen tab inside a screen               |
| ctrl+a [0-9]     | Switch to a screen tab by number 0 through 9          |
| ctrl+a n         | Go to the next screen tab                             |
| ctrl+a p         | Go to the previous screen tab                         |
| ctrl+a k         | Kill current screen tab                               |
