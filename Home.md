<h1 align="center">yabai</h1>
<p align="center">Tiling window management for the Mac.</p>
<p align="center">
    <img src="https://img.shields.io/badge/Platform-macOS-blue.svg?style=flat" alt="platform">
    <a href="https://github.com/koekeishiya/yabai/blob/master/LICENSE.txt"><img src="https://img.shields.io/github/license/koekeishiya/yabai.svg?color=blue" alt="license"></a>
    <a href="https://github.com/koekeishiya/yabai/blob/master/CHANGELOG.md"><img src="https://img.shields.io/badge/view-changelog-blue.svg" alt="changelog"></a>
    <a href="https://github.com/koekeishiya/yabai/releases"><img src="https://img.shields.io/github/commits-since/koekeishiya/yabai/latest.svg" alt="version"></a>
</p>

### What is yabai?

yabai is a tiling window manager for macOS High Sierra 10.13.6 and macOS Mojave 10.14.5. It automatically modifies your window layout using a binary space partitioning algorithm to allow you to focus on the content of your windows without distractions.

Integration with [&rightarrow;&nbsp;skhd][gh-skhd] allows you to become the macOS power user you have always wanted to be. Create custom keybindings to control windows, spaces and displays in practically no time and get your hands off the mouse and trackpad and back onto the keyboard where actual work gets done.

### Quickstart guide

yabai can be installed via Homebrew from a custom tap. It does, however, require you to disable System Integrity Protection ("rootless"), because it controls windows by acting through Dock.app&thinsp;—&thinsp;which is the sole owner of the main connection to the window server.

1. Disable System Integrity Protection
2. Install yabai and configure macOS to allow it to run
3. Configure yabai to your liking
4. Optional: Integrate yabai with other software like [&rightarrow;&nbsp;skhd][gh-skhd] for keyboard shortcuts or [&rightarrow;&nbsp;Übersicht][gh-uebersicht] for desktop widgets

You can find detailed instructions on every step of the quickstart guide in this wiki. The sidebar to the right (bottom for mobile devices) has a sorted list of pages with links to individual chapters. 

### Should you upgrade from chunkwm?

A commonly asked question is whether you should update from [&rightarrow;&nbsp;chunkwm][gh-chunkwm] to yabai right now. In general, the answer to this is yes. 

There are, however, a few notable exceptions: If you either cannot disable System Integrity Protection or are heavily invested into the plugin API and absolutely cannot replace your plugins using the signals and rules provided by yabai.

Please note that chunkwm will not work on macOS 10.15 Catalina.

### Comparison with other window managers

**NOTE:** This feature comparison table is far from complete. Please contribute. It's mostly a placeholder in its current state.

<!-- 
Useful HTML entities for this table:
- Check mark symbol: &#10003;
- Ballot X symbol:   &#10007;
--->

||yabai|[&rightarrow;&nbsp;chunkwm][gh-chunkwm]|[&rightarrow;&nbsp;Amethyst][gh-amethyst]|
|-:|:-:|:-:|:-:|
|**General**|
|Supported macOS versions|10.13–10.15|10.13–10.14|10.12–10.15|
|Works with SIP enabled|&#10007;|&#10003;*|&#10003;|
|Integrate with 3rd party tools|Signals, Rules and Commands|Rules and Commands**|&#10007;|
|Plugin API|&#10007;|&#10003;|&#10007;|
|**Windows**|
|Modify window properties|&#10003;|&#10003;|&#10007;|
|**Spaces**|
|Create and destroy spaces|&#10003;|&#10003;|&#10007;|
|Move spaces|&#10003;|&#10007;|&#10007;|
|**Displays**|
|Support multiple displays|&#10003;|&#10003;*|&#10003;*|


\* partially  
\*\* `chunkwm` commands have meaningless return values

[gh-skhd]: https://github.com/koekeishiya/skhd
[gh-uebersicht]: https://github.com/felixhageloh/uebersicht
[gh-chunkwm]: https://github.com/koekeishiya/chunkwm
[gh-amethyst]: https://github.com/ianyh/Amethyst