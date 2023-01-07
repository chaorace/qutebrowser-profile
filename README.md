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

## Other options

Here's the full options list (also available with `--help`):

```
  qutebrowser-profile - use qutebrowser with per-profile cache, session history, etc

USAGE
  qutebrowser-profile [--list] [--choose [--only-existing] | --load <name> | --new <name>] [qutebrowser args]
  
  --load <name>
    Load named profile and run qutebrowser.
    
  --new <name>
    Created named profile and launch qutebrowser with it. 

  --choose, -c
    If specified, the user is asked to select a profile via dmenu. If dmenu returns an empty string or non-zero 
    exit code (eg user pressed escape instead of choosing an option) the operation is aborted and qutebrowser 
    is not opened.
 
    The user can choose any existing profile or type the name of a new profile into dmenu to load qutebrowser
    in a new profile. See --only-existing below to restrict this.
    
    --allow-no-profile, -np SLOTNAME
    If specified, a special choice option will be provided that launches qutebrowser without applying any profiles.
    This is effectively identical to launching qutebrowser directly! No effect with --new option.

    SLOTNAME is an optional parameter that controls the name to be used for this special choice option (default: "default").
 
  --only-existing, -e
    If specified, and --choose is in operation, the user can only choose an existing profile.
 
  --list
    List all known profiles.
  
  --dmenu
    Override location of dmenu. Rofi is autodetected without you needing to set this.

  --set OPTION VALUE
    When used with --new, adds `qutebrowser --set` options in generated `.desktop` file.
    May be specified multiple times.
  
  --qutebrowser
    Override location of qutebrowser to call.

```

## Licence

See LICENSE file
