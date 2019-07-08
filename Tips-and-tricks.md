### Quickly restart the yabai launch agent

When running through `brew services`, restarting yabai using `brew services restart yabai` can take a few seconds. You can achieve (almost) the same effect by running this command instead:

```sh
launchctl kickstart -k "gui/${UID}/homebrew.mxcl.yabai"

# e.g. bind to key in skhd:
# ctrl + alt + cmd - r : launchctl kickstart -k "gui/${UID}/homebrew.mxcl.yabai"
```

### Split yabai configuration across multiple files

The below script loads all executable files (`chmod +x`) in `~/.config/yabai/` and executes them. Why? Because then parts of your config can be reloaded individually from signals or external triggers.

```sh
# find all executable files in ~/.config/yabai and execute them
find "${HOME}/.config/yabai" -type f -perm +111 -exec {} \;
```

### Fix folders opened from desktop not tiling

When opening a folder on the desktop there's an animation that conflicts with yabai trying to tile the window. This animation can be disabled:

```sh
defaults write com.apple.finder DisableAllAnimations -bool true
killall Finder # or logout and login

# to reset system defaults, delete the key instead
# defaults delete com.apple.finder DisableAllAnimations
```

### Fix spaces reordering automatically

In System Preferences, navigate to Mission Control and uncheck the option "Automatically rearrange Spaces based on most recent use". 


### Auto updating from HEAD via brew

The below snippet makes yabai check for updates whenever it starts and automatically installs them for you, only requiring you to enter your password. Just put it at the end of your yabai configuration file and forget about it.

Note that this is only installations from HEAD (`brew install yabai --HEAD`).

<details>
<summary>Click to expand snippet</summary>

#### Method 1

This downloads an up-to-date version of the yabai autoupdate script hosted by [@dominiklohmann](https://github.com/dominiklohmann) and executes it whenever yabai starts.

```sh
YABAI_CERT=yabai-cert sh -c "$(curl -fsSL "https://git.io/update-yabai")" &
```

#### Method 2

This does the same as above, except the update snippet doesn't update itself. Check back for changes. Last update: 2019-07-04.

```sh
# set codesigning certificate name here (default: yabai-cert)
YABAI_CERT=

function main() {
    if check_for_updates; then
        install_updates ${YABAI_CERT}
    else
        osascript << EOM
            display notification "Configuration loaded." ¬
                with title "$(yabai --version)"
EOM
    fi
}

# Please do not touch the code below unless you absolutely know what you are
# doing. It's the result of multiple long evenings trying to get this to work
# and relies on terrible hacks to work around limitations of launchd.
# For questions please reach out to @dominiklohmann via GitHub.

function check_for_updates() {
    set -o pipefail

    installed="$(brew info koekeishiya/formulae/yabai | grep 'HEAD-' \
        | awk '{print substr($1,length($1)-6)}')"
    remote="$(git ls-remote 'https://github.com/koekeishiya/yabai.git' HEAD \
        | awk '{print substr($1,1,7)}')"

    [ ${?} -eq 0 ] && [[ "${installed}" != "${remote}" ]]
}

function install_updates() {
    script=$(mktemp)

    cat > ${script} << EOF
        #! /usr/bin/env sh

        clear
        printf "\e[3J\e[1mUpdating yabai...\e[0m\n"
        printf "Authenticate to continue, Ctrl+C to cancel.\n\n"

        if sudo -v; then
            brew services stop koekeishiya/formulae/yabai
            brew reinstall koekeishiya/formulae/yabai
            codesign -fs "${1:-yabai-cert}" "$(brew --prefix yabai)/bin/yabai"
            sudo yabai --uninstall-sa
            sudo yabai --install-sa
            brew services start koekeishiya/formulae/yabai
            killall Dock
            sleep 2
            clear
            printf "\e[3J"
        fi

        ps -eo pid,comm | grep -v grep | grep -i Terminal | tail -1 \
            | awk '{print $1}' | xargs kill
EOF

    chmod +x ${script}
    open -FWnb com.apple.Terminal ${script}
    rm -f ${script}
}

main &
```

</details>

### Tiling Emacs

Emacs is not a well-behaved citizen of macOS. Try using [&rightarrow;&nbsp;emacs-mac](https://bitbucket.org/mituharu/emacs-mac) from the Homebrew tap [&rightarrow;&nbsp;emacsmacport](https://github.com/railwaycat/homebrew-emacsmacport) and add the following line to your configuration file to get yabai to recognize Emacs.

```emacs-lisp
(menu-bar-mode t)
```