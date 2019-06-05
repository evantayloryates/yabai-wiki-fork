If you want to run the latest and greatest version of yabai, you can install off of `HEAD`. Note that this will require codesigning with a self-signed certificate, so you'll have to create one first (and only once).

First, open `Keychain Access.app`. In its menu, navigate to `Keychain Access`, then `Certificate Assistance`, then click `Create a Certificate...`. This will open the `Certificate Assistant`. Choose these options:

- Name: `yabai-cert`,
- Identity Type: `Self-Signed Root`
- Certificate Type: `Code Signing`

Click `Create`, then `Continue` to create the certificate.

Now onto installing *yabai*:

```sh
brew install koekeishiya/formulae/yabai --HEAD
codesign -fs 'yabai-cert' $(which yabai)
```

Now run *yabai* once. It will quit and show a dialog asking for accessibility permissions.

Either click `Open System Preferences` or manually open `System Preferences.app` and navigate to `Security & Privacy`, then `Privacy`, then `Accessibility`.

Click the lock icon at the bottom and enter your password to allow changes to the list and check the box next to *yabai*. If *yabai* is not already in the list, add *yabai* manually by using the `+` labelled button. When installed using Homebrew, *yabai* will usually be at `/usr/local/bin/yabai`.

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
# stop, reinstall, codesign, start yabai
brew services stop yabai
brew reinstall yabai
codesign -fs 'yabai-cert' $(which yabai)
brew services start yabai

# reinstall the scripting addition
sudo yabai --uninstall-sa
sudo yabai --install-sa

# load the scripting addition
pkill Dock
```

### Getting notified about available updates

If you want `yabai` to notify you when an update is available, add the following code to your `~/.yabairc` file. Note that this requires you to install `jq` and `terminal-notifier`, both of which are available from Homebrew.

```sh
function check_for_updates() {
        set -o pipefail
        installed="$(brew info --json koekeishiya/formulae/yabai | jq -r '.[0].installed[0].version')"
        remote="HEAD-$(git ls-remote https://github.com/koekeishiya/yabai.git HEAD | awk '{print substr($1,1,7)}')"

        if [ ${?} -ne 0 ]; then
                terminal-notifier -title "$(yabai --version)" -message "Failed to check for updates"
        elif [[ "${installed}" == "${remote}" ]]; then
                terminal-notifier -title "$(yabai --version)" -message "Configuration loaded"
        else
                terminal-notifier -title "$(yabai --version)" -message "There is an update available for yabai"
        fi
}

check_for_updates &
```