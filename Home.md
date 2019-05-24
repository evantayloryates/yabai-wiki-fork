## Welcome to the _yabai_ wiki!

This wiki page services as a community–driven documentation page. 

If you find anything you want to improve or add, feel free to do so. Currently, this wiki is free for anyone to edit, although this might change at a later point.

If you want to request a topic for this wiki to address, head over to [issue #5](https://github.com/koekeishiya/yabai/issues/5).

## What is *yabai*?

*yabai* us a tiling window manager for macOS 10.14 and above. It automatically modifies your window layout using a binary space partitioning algorithm to allow you to focus on the content of your windows without having to 

Integration with [*skhd*](https://github.com/koekeishiya/skhd) allows you to become the macOS power user you have always wanted to be. Create custom keybindings to control windows, spaces and displays in practically no time and get your hands off the mouse and trackpad and back onto the keyboard where actual work gets done.

## Quickstart guide

*yabai* can be installed via Homebrew from a custom tap. It does, however, require you to disable *System Integrity Protection* ("rootless"), because it controls windows by acting through _Dock.app_—which is the sole owner of the main connection to the window server.

- Disable *System Integrity Protection*
- Install _yabai_
- Allow _yabai_ to control your device using accessibility features
- Install the scripting addition
- Run yabai and restart _Dock.app_

You can find detailed instructions on every step of the quickstart guide in this wiki.