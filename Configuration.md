A short and concise overview of options available with your current installation is available using `man yabai` or for the current development version as a [&rightarrow;&nbsp;rendered document][docs-config].

This wiki page aims to explain every configuration option in detail. 

### Configuration file

The per–user yabai configuration file must be named `.yabairc`, must be in your home–directory and must be executable. It's just a shell script that's ran before yabai reads its configuration options.

```sh
# create empty configuration file and make it executable
touch ~/.yabairc
chmod +x ~/.yabairc
```

### Tiling options

#### Layout

Layout defines whether windows are tiled ("managed", "bsp") by yabai or left alone ("float"). This setting can be defined on a per–space basis.

```sh
# bsp or float (default: bsp)
yabai -m config layout bsp

# Override default layout for space 2 only
yabai -m config --space 2 layout float
```

#### Padding and gaps

When tiling windows, yabai can maintain gaps between windows and padding towards menu bar, dock and screen edges. This setting can be defined on a per–space basis.

```sh
# Set all padding and gaps to 20pt (default: 0)
yabai -m config top_padding    20
yabai -m config bottom_padding 20
yabai -m config left_padding   20
yabai -m config right_padding  20
yabai -m config window_gap     20

# Override gaps for space 2 only
yabai -m config --space 2 window_gap 0
```

#### Split ratios

Auto balance makes it so all windows always occupy the same space, independent of how deeply nested they are in the window tree. When a new window is inserted or a window is removed, the split ratios will be automatically adjusted.

```sh
# on or off (default: off)
yabai -m config auto_balance off
```

If auto balance is disabled, the split ratio defines how much space each window occupies after a new split is created. A value of 0.5 means that both old and new window occupy the same space; a value of 0.2 means that the old window occupies 20% of the available space and the new window occupies 80% of the available space. New windows are inserted at the right or bottom side. The ratio needs to be between 0 and 1.

```sh
# Floating point value between 0 and 1 (default: 0.5)
yabai -m config split_ratio 0.5
```

### Mouse support

When you drag a tiled window onto another, yabai swaps their positions in the window tree.

### Window modifications

### Status bar

[docs-config]: https://github.com/koekeishiya/yabai/blob/master/doc/yabai.asciidoc#config