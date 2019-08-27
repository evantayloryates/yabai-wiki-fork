A codesigned binary release of yabai can be installed using Homebrew from the tap `koekeishiya/formulae`.

```sh
brew install koekeishiya/formulae/yabai
```

Open `System Preferences.app` and navigate to `Security & Privacy`, then `Privacy`, then `Accessibility`. Click the lock icon at the bottom and enter your password to allow changes to the list. Starting with `brew services start yabai` will prompt the user to allow `yabai` accessibility permissions. Check the box next to `yabai` to allow accessibility permissions.

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
killall Dock
```

### Updating to the latest release

To update yabai to the latest version, simply upgrade it with Homebrew, reinstall the scripting addition and restart *Dock.app* again:

```sh
# stop, upgrade, start yabai
brew services stop yabai
brew upgrade yabai
brew services start yabai

# reinstall the scripting addition
sudo yabai --uninstall-sa
sudo yabai --install-sa

# load the scripting addition
killall Dock
```