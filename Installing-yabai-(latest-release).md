A codesigned binary release of *yabai* can be installed using Homebrew from the tap `koekeishiya/formulae`.

```sh
brew install koekeishiya/formulae/yabai
```

Now run *yabai* once. It will quit and show a dialog asking for accessibility permissions.

Either click `Open System Preferences` or manually open `System Preferences.app` and navigate to `Security & Privacy`, then `Privacy`, then `Accessibility`.

Click the lock icon at the bottom and enter your password to allow changes to the list and check the box next to `yabai`. If *yabai* is not already in the list, add `yabai` manually by using the `+` labelled button. When installed using Homebrew, *yabai* will usually be at `/usr/local/bin/yabai`.

Now install the scripting addition.

```sh
# install the scripting addition
sudo yabai --install-sa
```

To run yabai, simply start it and then restart *Dock.app* to load the scripting addition. Alternatively you can also logout and login again.

```sh
# start yabai
brew services start yabai

# load the scripting addition
pkill Dock
```

To upgrade yabai to the latest version, simply upgrade it with Homebrew, reinstall the scripting addition and restart *Dock.app* again:

```sh
# stop, upgrade, start yabai
brew services stop yabai
brew upgrade yabai
brew services start yabai

# reinstall the scripting addition
sudo yabai --uninstall-sa
sudo yabai --install-sa

# load the scripting addition
pkill Dock
```