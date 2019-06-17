### What is yabai?

yabai is a tiling window manager for macOS High Sierra 10.13.6 and macOS Mojave 10.14.5. It automatically modifies your window layout using a binary space partitioning algorithm to allow you to focus on the content of your windows without distractions.

Integration with [&rightarrow;&nbsp;skhd][gh-skhd] allows you to become the macOS power user you have always wanted to be. Create custom keybindings to control windows, spaces and displays in practically no time and get your hands off the mouse and trackpad and back onto the keyboard where actual work gets done.

### Quickstart guide

yabai can be installed via Homebrew from a custom tap. It does, however, require you to disable System Integrity Protection ("rootless"), because it controls windows by acting through Dock.app&thinsp;—&thinsp;which is the sole owner of the main connection to the window server.

- Disable System Integrity Protection
- Install yabai and configure macOS to allow it to run
- Configure yabai to your liking
- Optional: Integrate yabai with other software like [&rightarrow;&nbsp;skhd][gh-skhd] for keyboard shortcuts or [&rightarrow;&nbsp;Übersicht][gh-uebersicht] for desktop widgets

You can find detailed instructions on every step of the quickstart guide in this wiki. The sidebar to the right (bottom for mobile devices) has a sorted list of pages with links to individual chapters. 

[gh-skhd]: https://github.com/koekeishiya/skhd
[gh-uebersicht]: https://github.com/felixhageloh/uebersicht