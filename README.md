# Third-party Apt repository sources

Quick and easy Apt repositories

## Introduction

This is a collection of apt .sources files for third-party apt repositories; third-party in this case meaning 'not part of the main Ubuntu repo'. This includes:

1. Apt repos by third-parties, like Mozilla or Microsoft
2. Apt repos by first-parties, like the Ubuntu Git Maintainers team, but which are hosted separately on PPAs

## Installation

Easy peasy, just find the .sources file you want and put it in your `/etc/apt/sources.list.d` directory, then `apt update`. Each sources file contains the ASCII-armored GPG key for the repository so you don't need to import the GPG key separately.

All of these files are currently configured for Ubuntu Noble; if you're running a different Ubuntu release you may have to edit the files (I'll be working on doing this later).

## Caveats

There are also some caveats with some of the repositories that you might need to do to make them work properly.

### 1password

The 1password post-install script will create a file at `/etc/apt/sources.list.d/1password.list` which references the same repository as this .sources file, and that confuses/breaks apt. You can fix this one of two ways:

1. Remove the .sources file after you install 1password, which is annoying to have to do
2. Symlink the file to `/dev/null` by running `ln -sf /dev/null /etc/apt/sources.list.d/1password.list`, which produces the following warning message every single time you use apt for anything:

```
N: Ignoring '1password.list' in directory '/etc/apt/sources.list.d/' as it is not a regular file
```

### Mozilla

Add the following to `/etc/apt/preferences.d/no-ubuntu-firefox` to prevent Ubuntu from replacing your apt-installed firefox with the snap version.

```
Package: firefox
Pin: release l=Ubuntu
Pin-Priority: -1
```
