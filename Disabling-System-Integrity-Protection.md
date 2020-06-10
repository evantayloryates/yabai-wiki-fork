### What is System Integrity Protection and why does it need to be disabled?

System Integrity Protection ("rootless") is a security feature of macOS first introduced in 10.13, then further locked down in 10.14.

System Integrity Protection protects some files and directories from being modified&thinsp;—&thinsp;even from the root user. yabai needs System Integrity Protection to be (partially) disabled so that it can inject a scripting addition into Dock.app, which owns the sole connection to the macOS window server. Many features of yabai require this scripting addition to be running such that yabai can modify windows, spaces and displays in a way that otherwise only Dock.app could.

The following features of yabai require System Integrity Protection to be (partially) disabled:

* focus/create/destroy space without animation
* move space (and its windows) left, right or to another display
* remove window shadows
* enable window transparency
* control window layers (make windows appear topmost)
* sticky windows (make windows appear on all spaces)
* move window by clicking anywhere in its frame
* toggle picture-in-picture for any given window
* border for focused and inactive windows

### How do I disable System Integrity Protection?

1. Turn off your device
2. Hold down <kbd>command ⌘</kbd><kbd>R</kbd> while booting your device.
3. In the menu bar, choose `Utilities`, then `Terminal`
4.
```bash
# If you're on macOS 10.14 and above
# (printed warning can be safely ignored)
csrutil enable --without debug --without fs

# If you're on macOS 10.13
# (disables SIP completely)
csrutil disable
```

5. Reboot
6. You can verify that System Integrity Protection is turned off by running `csrutil status`, which returns `System Integrity Protection status: disabled.` if it is turned off

If you are running yabai on macOS 10.13.6 (High Sierra) you can and should re–enable System Integrity Protection after the installation has completed. Repeat the steps above, but run `csrutil enable` instead at step 4.
The same instructions apply if you ever want to re–enable System Integrity Protection after uninstalling yabai.

Please note that System Integrity Protection will be re–enabled during device repairs or analysis at any Apple Retail Store or Apple Authorized Service Provider. You will have to repeat this step after getting your device back.