# Rainbow Dash Boot Animation
This is a plymouth theme featuring animation of rainbow dash flying. The prebuilt `.deb` package is for **debian-based operating systems** (Debian, Ubuntu, Kali Linux, Linux Mint and others). Arch Linux is supported through the [AUR-style packages](#arch-linux). **Non-Linux systems like Windows, iPhone and Android can't install this**.

## Download
Open release section to [download](https://github.com/yeaayy/plymouth-theme-rainbow-dash/releases/latest).

## Themes
This package installs two themes:
 - **Rainbow Dash Flying** (`rainbow-dash`) — light sky background. This is set as the default during installation.
 - **Rainbow Dash Dark** (`rainbow-dash-dark`) — dark night-sky background.

To switch to the dark theme run:
```sh
sudo plymouth-set-default-theme rainbow-dash-dark -R
```
To switch back to the light theme run:
```sh
sudo plymouth-set-default-theme rainbow-dash -R
```

## Building
Just run
```sh
./build
```
from project root directory and it should output the package to `plymouth-theme-rainbow-dash_<version>_all.deb`. Where `<version>` is version of the theme (currently it).

## Installing
After download or build the package run
```sh
sudo dpkg -i plymouth-theme-rainbow-dash_<version>_all.deb
```

## Removing
```sh
sudo dpkg -r plymouth-theme-rainbow-dash
```

## Temporary Removal
### Temporary Removal on Kali Linux
To temporarily switch back to default Kali Linux boot animation run
```sh
sudo plymouth-set-default-theme kali -R
```
---
To switch back again to this boot animation run
```sh
plymouth-set-default-theme rainbow-dash -R
```

### Temporary Removal on Linux Mint
```sh
sudo update-alternatives --config default.plymouth
```
choose  `/usr/share/plymouth/themes/mint-logo/mint-logo.plymouth`, then run:
```sh
sudo update-initramfs -c -k $(uname -r)
```
---
To switch back again to this boot animation run:
```sh
sudo update-alternatives --config default.plymouth
```
choose  `/usr/share/plymouth/themes/rainbow-dash/rainbow-dash.plymouth` or choose 0, then run
```sh
sudo update-initramfs -c -k $(uname -r)
```

## Arch Linux
Arch Linux is supported through `makepkg` (AUR-style) packages. Two packages are provided:

 - `plymouth-theme-rainbow-dash` — tracks the latest release.
 - `plymouth-theme-rainbow-dash-git` — tracks the git repository.

Build and install one locally from the project root:
```sh
cd plymouth-theme-rainbow-dash-git
makepkg -si
```
Then select a theme. The `-R` flag rebuilds the initramfs:
```sh
sudo plymouth-set-default-theme -R rainbow-dash
# or
sudo plymouth-set-default-theme -R rainbow-dash-dark
```

Plymouth on Arch also requires the `plymouth` hook in `/etc/mkinitcpio.conf` and the `splash` kernel parameter. See the [Arch Wiki](https://wiki.archlinux.org/title/Plymouth) for details.

### UKI (systemd-stub) splash

For UKI boots the package ships a static splash BMP for systemd-stub at
`/usr/share/plymouth/themes/rainbow-dash-dark/splash.bmp` (in the theme dir,
not `/usr/share/systemd/bootctl/`, which pacman cannot own). Point the preset
at it and rebuild the initramfs:

```sh
# /etc/mkinitcpio.preset
default_options="--splash /usr/share/plymouth/themes/rainbow-dash-dark/splash.bmp"
```

The dark theme animates the hand-off from this splash: the wordmark fades out
in place while the pony starts at the splash position and flies to the
animation centre.

## Test
This package is tested on:
 - Linux Mint
 - Kali Linux (VM)

I haven't try on other distro so if you try to install this package in other distro that aren't mentioned above please let me know, I will update the list and possibly fix it if it doesn't work.
