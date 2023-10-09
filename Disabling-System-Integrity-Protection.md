### What is System Integrity Protection and why does it need to be disabled?

System Integrity Protection ("rootless") is a security feature of macOS first introduced in 10.13, then further locked down in 10.14.

System Integrity Protection protects some files and directories from being modified&thinsp;—&thinsp;even from the root user. yabai needs System Integrity Protection to be (partially) disabled so that it can inject a scripting addition into Dock.app, which owns the sole connection to the macOS window server. Many features of yabai require this scripting addition to be running such that yabai can modify windows, spaces and displays in a way that otherwise only Dock.app could.

The following features of yabai require System Integrity Protection to be (partially) disabled:

* focus/move/swap/create/destroy space
* remove window shadows
* enable window transparency
* enable window animations
* control window layers (make windows appear topmost or on the desktop)
* sticky windows (make windows appear on all spaces on the display that contains the window)
* toggle picture-in-picture for any given window

See [this comment](https://github.com/koekeishiya/yabai/issues/1863) for a more in-depth explanation.

### How do I disable System Integrity Protection?

1. Turn off your device
&nbsp;
2. Boot system in Recovery Mode (see options below)
   &nbsp;
   **Intel Chip [(apple docs)](https://support.apple.com/en-gb/guide/mac-help/mchl338cf9a8/12.0/mac/12.0)**
   Hold down <kbd>command ⌘</kbd><kbd>R</kbd> while booting your device.
   &nbsp;
   **Apple Silicon [(apple docs)](https://support.apple.com/en-gb/guide/mac-help/mchl82829c17/12.0/mac/12.0):**
   Press and hold the power button on your Mac until “Loading startup options” appears.  
   Click Options, then click Continue.
   &nbsp;
3. In the menu bar, choose `Utilities`, then `Terminal`
&nbsp;

4. Partially remove integrity protections (see options below)[^1][^2]
   &nbsp;
   **Intel—MacOS 11,12 or 13**
   ```bash
   # Requires Filesystem Protections and Debugging Restrictions to be disabled (workaround because --without debug does not work)
   # (printed warning can be safely ignored)
   csrutil disable --with kext --with dtrace --with nvram --with basesystem
   ```
   &nbsp;
   **Apple Silicon—MacOS 12**
   ```bash
   # Requires Filesystem Protections, Debugging Restrictions and NVRAM Protection to be disabled
   # (printed warning can be safely ignored)
   csrutil disable --with kext --with dtrace --with basesystem
   ```
   &nbsp;
   **Apple Silicon—MacOS 13**
   ```bash
   # Requires Filesystem Protections, Debugging Restrictions and NVRAM Protection to be disabled
   # (printed warning can be safely ignored)
   csrutil enable --without fs --without debug --without nvram
   ```
   &nbsp;
5. Reboot
&nbsp;
6. _(Apple Silicon only)_ Enable non-Apple-signed arm64e binaries
&nbsp;
   1. Run the terminal command ```sudo nvram boot-args=-arm64e_preview_abi```
   2. Reboot
   &nbsp;
7. You can verify that System Integrity Protection is turned off by running `csrutil status`, which returns `System Integrity Protection status: disabled.` if it is turned off (it may show `unknown` for newer versions of macOS when disabling SIP partially).
&nbsp;

[^1]: If you ever want to re–enable System Integrity Protection after uninstalling yabai; repeat the steps above, but run `csrutil enable` instead at step 4.
[^2]: Please note that System Integrity Protection will be re–enabled during device repairs or analysis at any Apple Retail Store or Apple Authorized Service Provider. You will have to repeat this step after getting your device back.
