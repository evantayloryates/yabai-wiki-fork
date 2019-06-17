### What is *System Integrity Protection* and why does it need to be disabled?

*System Integrity Protection* ("rootless") is a security feature of macOS first introduced in 10.13, then further locked down in 10.14.

*System Integrity Protection* protects some files and directories from being modified—even from the root user. *yabai* needs *System Integrity Protection* to be disabled so that it can inject a scripting addition into *Dock.app*, which owns the sole connection to the macOS window server. Many features of *yabai* require this scripting addition to be running such that *yabai* can modify windows, spaces and displays in a way that otherwise only *Dock.app* could.

### How do I disable *System Integrity Protection*?

1. Turn off your device
2. Hold down <kbd>command ⌘</kbd><kbd>R</kbd> while booting your device.
3. In the menu bar, choose `Utilities`, then `Terminal`
4. Run the command `csrutil disable`
5. Reboot
6. You can verify that *System Integrity Protection* is turned off by running `csrutil status`, which returns `System Integrity Protection status: disabled.` if it is turned off