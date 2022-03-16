A codesigned binary release of yabai can be installed using Homebrew from the tap `koekeishiya/formulae`.

```sh
brew install koekeishiya/formulae/yabai
```

Open `System Preferences.app` and navigate to `Security & Privacy`, then `Privacy`, then `Accessibility`. Click the lock icon at the bottom and enter your password to allow changes to the list. Starting with `brew services start yabai` will prompt the user to allow `yabai` accessibility permissions. Check the box next to `yabai` to allow accessibility permissions.

Now install the scripting addition.

```sh
# install the scripting addition
sudo yabai --install-sa

# if macOS Big Sur or Monterey, load the scripting addition manually; follow instructions below to automate on startup
sudo yabai --load-sa
```

To run yabai, simply start it. 

```sh
# start yabai
brew services start yabai
```

### macOS Big Sur - Automatically load scripting addition on startup

In macOS Big Sur we had to switch to using the mach API to inject the scripting addition. Injection now has to run with elevated (root) privileges, meaning that yabai is no longer able to automatically load the scripting addition during startup. However, you can use the following workaround to make it pretty much as seamless as it used to be. The trick is to allow your user to execute *yabai --load-sa* as the root user without having to enter a password. To do this, we add a new configuration entry that is loaded by */etc/sudoers*.

```
# create a new file for writing - visudo uses the vim editor by default.
# go read about this if you have no idea what is going on.
sudo visudo -f /private/etc/sudoers.d/yabai

# input the line below into the file you are editing.
# replace <user> with your username (output of: whoami). 
# change the path to the yabai binary if necessary  (output of: which yabai)
<user> ALL = (root) NOPASSWD: /usr/local/bin/yabai --load-sa
```

After the above edit has been made, simply add the command to load the scripting addition to the top of your yabairc config file

```
# the scripting-addition must be loaded manually if
# you are running yabai on macOS Big Sur. Uncomment
# the following line to have the injection performed
# when the config is executed during startup.
#
# for this to work you must configure sudo such that
# it will be able to run the command without password

sudo yabai --load-sa
yabai -m signal --add event=dock_did_restart action="sudo yabai --load-sa"

# .. more yabai startup stuff
```

### Updating to the latest release

To update yabai to the latest version, simply upgrade it with Homebrew and reinstall the scripting addition:

```sh
# stop, and upgrade yabai
brew services stop yabai
brew upgrade yabai

# uninstall the scripting addition
sudo yabai --uninstall-sa

# installing the scripting addition will restart Dock.app
sudo yabai --install-sa

# finally, start yabai
brew services start yabai
```