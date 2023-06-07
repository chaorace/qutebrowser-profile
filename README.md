# qutebrowser-profile

A wrapper script for qutebrowser that allows you to maintain different profiles, each with their own history and session state but sharing the same `config.py`.

## Why?

I use my system for different projects and purposes, such as *email*, *cloud development*, *web browsing* and so on. Using `qutebrowser-profile` I can keep all of these in separate qutebrowser profiles.

## Credit
This fork is maintained by [Christopher Crockett](https://github.com/chaorace/qutebrowser-profile)

Base package written by [Jonny Tyers](https://github.com/jtyers/qutebrowser-profile)

Original concept by [ayekat](https://github.com/ayekat/dotfiles/blob/master/bin/qutebrowser)

## Installation
The `qutebrowser-profile` is written in bash-flavored shell script. Please ensure your environment is compatible before proceeding!

The `--choose` feature depends upon either the `dmenu` or `rofi` package (Rofi is preferred). You may still use `--load`/`--new` without these dependencies, however. When both `rofi` *and* `dmenu` are installed, `rofi` is prioritized. You may force usage of `dmenu` (or any other dmenu-compatible alternative) via the `--dmenu` flag (e.g. `--dmenu="dmenu"`).

### All platforms
Clone this repository and add it to your `$PATH`.

NOTE: To update, you will need to run `git pull` from within the repository

### Arch-based Linux
#### Option A: Install package file
Download the latest release "pkg.tar.zst" file from [Releases](https://github.com/chaorace/qutebrowser-profile/releases) and install using `pacman -U [PACKAGE FILE]`

NOTE: To update, you will need to download the latest release and install the file again via `pacman -U [PACKAGE FILE]`
#### Option B: Install via repo
Edit `/etc/pacman.conf`, add an entry for this package's dedicated Arch repository:
```
[qutebrowser-profile-chao]
SigLevel = Optional TrustAll
Server = https://chaorace.github.io/qutebrowser-profile/pool
```

Finally, install via `pacman -S qutebrowser-profile-chao`

NOTE: Installing this way will cause the package to automatically update when running `pacman -Syu`. Please only use this method if you find that to be acceptable!

## Getting started

To create a new profile, just call the script:

`qutebrowser-profile`

You'll get a rofi/dmenu prompt asking for a profile name. Type one in and hit enter, and qutebrowser will load your profile.

## Features

 * qutebrowser's window will have `[my-profile-name]` at the start, so you can easily distinguish different qutebrowsers loaded with different profiles
 * qutebrowser loads configuration from the normal location (and all qutebrowsers share configuration regardless of profile, this includes quickmarks/bookmarks)
   * If you need some profile-specific configuration like a custom downloads directory, using the `--set` option with `--new` will set these in the generated `.desktop` file.
 * other data, such as session history, cache, cookies, etc, will be unique to that profile
 * A new `.desktop` file will be created for each profile, allowing you to launch each one using a GUI launcher. Name will be "Qute [$profile]"
 * Each profile will be treated as a unique app by the window managers because we set a unique WM\_CLASS for X11 and a unique app\_id for Wayland (requires Qutebrowser > 1.14.1).
 * The same Qutebrowser icon is used for the new profiles, but you can reference your own by editing `~/.local/share/applications/qutebrowser-$profile.desktop`.

## Usage

### Syntax
```
qutebrowser-profile [Main Argument] [Option Arguments] [qutebrowser Arguments]
```
### Main Arguments
Only one of these may be used. `--choose` is the default.
* `--list`, `-l`

    Prints profiles to output. May be combined with another main argument.

    Only non-hidden profiles will be shown. See `--show-hidden` for lifting this restriction.
* `--load <name>`, `-p <name>`

    Directly load profile called `<name>`.
* `--new <name>`, `-n <name>`

    Directly create and load profile called `<name>`.
* `--choose`, `-c`

    Prompt the user to select a profile via dmenu/Rofi. Arbitrary name inputs are also accepted, which will either create a new profile with the given name or launch a matching hidden profile.

    Only non-hidden profiles will be shown. See `--show-hidden` for lifting this restriction.

    If dmenu/Rofi returns an empty string or non-zero exit code (e.g.: user pressed escape instead of choosing an option), qutebrowser will not be opened.

### Option Arguments

* `--allow-no-profile [<slotname>]`, `-np [<slotname>]`

    Applies to: `--choose`, `--load`

    If specified, a special choice option called `<slotname>` will be provided which launches qutebrowser without applying any profiles.

    `<slotname>` is an optional parameter that controls the name to be used for this special choice option (default: "default").
* `--dmenu <path>`

    Override location of dmenu executable. Rofi is autodetected without you needing to set this.
* `--only-existing`, `-e`

    Applies to: `--choose`

    Prevents creating new profiles by manually entering a name into the prompt.
* `--qutebrowser <path>`

    Override location of qutebrowser executable.
* `--set OPTION VALUE`

    Sets qutebrowser configuration settings for the session. May be specified multiple times.
    
    No effect if a qutebrowser session is already running for selected profile.
* `--show-hidden`, `-a`

    Applies to: `--list`, `--choose`

    If specified, normally hidden profiles (i.e.: has a name starting in ".") will be included in the resulting list/prompt.

    When used with --new, the given configuration will also be embedded into the generated XDG Desktop file.

* `--suppress-info`

    If specified, prevents info messages from printing to output.

    This is useful when using the program a protocol handler if certain applications (e.g.: Slack) treat log output as a launch failure.
## Licence

See LICENSE file
