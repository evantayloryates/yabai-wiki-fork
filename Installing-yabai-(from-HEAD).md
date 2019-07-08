If you want to run the latest and greatest version of yabai, you can install off of `HEAD`. Note that this will require codesigning with a self-signed certificate, so you'll have to create one first (and only once).

First, open `Keychain Access.app`. In its menu, navigate to `Keychain Access`, then `Certificate Assistance`, then click `Create a Certificate...`. This will open the `Certificate Assistant`. Choose these options:

- Name: `yabai-cert`,
- Identity Type: `Self-Signed Root`
- Certificate Type: `Code Signing`

Click `Create`, then `Continue` to create the certificate.

Now onto installing yabai:

```sh
brew install koekeishiya/formulae/yabai --HEAD
codesign -fs 'yabai-cert' $(which yabai)
```

Open `System Preferences.app` and navigate to `Security & Privacy`, then `Privacy`, then `Accessibility`. Click the lock icon at the bottom and enter your password to allow changes to the list. Add `yabai` manually by using the `+` labelled button. When installed using Homebrew, yabai will usually be at `/usr/local/bin/yabai`. Check the box next to `yabai` to allow accessibility permissions.

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

### Updating to latest HEAD

To upgrade yabai to the latest version from HEAD, simply reinstall it with Homebrew, codesign it, reinstall the scripting addition and restart *Dock.app* again:

```sh
# set codesigning certificate name here (default: yabai-cert)
export YABAI_CERT=

# stop yabai
brew services stop koekeishiya/formulae/yabai

# reinstall yabai
brew reinstall koekeishiya/formulae/yabai
codesign -fs "${YABAI_CERT:-yabai-cert}" "$(brew --prefix yabai)/bin/yabai"

# reinstall the scripting addition
sudo yabai --uninstall-sa
sudo yabai --install-sa

# start yabai
brew services start koekeishiya/formulae/yabai

# load the scripting addition
killall Dock
```