
# Basic System Setup

## Fix luks setup during installation
The calamares installer creates a luks configuration that is incompatible with GRUB's capabilities. After the installer has finished but before the reboot you need to apply the following fix:
    cryptsetup luksChangeKey --pbkdf pbkdf2 /dev/nvme0n1p2
    cryptsetup luksChangeKey --pbkdf pbkdf2 /dev/nvme0n1p3

## Skip grub menu on startup
In `/etc/default/grub`, set GRUB_TIMEOUT to 0

## Enable autologin
In `/etc/sddm.conf`, in the "[Autologin]" section, add the line "User=<username>"

## Make Power settings
In `/etc/systemd/logind.conf`:
  HandlePowerKey=ignore
  HandlePowerKeyLongPress=poweroff
  PowerKeyIgnoreInhibited=yes

## Fix shell shortcuts
I recommend to remove all aliases to eza, bat, cat, etc. because of insane defaults that actually make your life hard in ways you wouldn't expect. Check out:
- `/usr/share/garuda/garuda-bash-config/bashrc`
- `/usr/share/garuda/garuda-fish-config/config.fish`

## Home cleanup
rmdir Public Templates Videos Projects Pictures

## Install essentials
Install some essentials before loading the config:

    pacman -S batsignal mdp mpc rmpc rofi wallust wlogout yazi cava wev
    yay -S zscroll

## Install config 
Load various configs for the desktop environment

    git clone https://github.com/igsor/arch-garuda-hyprland-dotfiles.git .config/

## Autostart system services
Start some services by default

    systemctl --user enable mdp.service
    systemctl --user enable batsignal.service

## Install neovim
Install neovim and load the config

    pacman -S neovim
    git clone github.com/igsor/neovim-config .config/nvim

Follow the neovim config's readme at `.config/nvim/README.md`

## Install common software
You might have installed some of those during the finalization of the installation (after first boot).
Otherwise, install them manually.

    pacman -S extra/vlc-plugin-ffmpeg firefox guvcview keepassxc mplayer okular pdftk puzzles python-virtualenv scribus sshfs thunderbird tree vlc-plugins-base
    pacman -R firedragon


# Keybindings

## Application
<SUPER-SPACE>                                 Application launcher
<POWERBTN>                                    Logout/Exit screen
<SUPER-Q>                                     Close active window
<SUPER-E>                                     file browser
<SUPER-F>                                     web browser
<SUPER-S>                                     text editor
<SUPER-T>                                     Terminal

## Window location
<SUPER-[DOWN|J]>                              Select window below
<SUPER-[LEFT|H]>                              Select window to the left
<SUPER-[RIGHT|L]>                             Select window to the right
<SUPER-[UP|K]>                                Select window above
<SUPER-SHIFT-[DOWN|J]>                        Move window down
<SUPER-SHIFT-[LEFT|H]>                        Move window left
<SUPER-SHIFT-[RIGHT|L]>                       Move window right
<SUPER-SHIFT-[UP|K]>                          Move window up
<SUPER-SHIFT-[1-0]>                           Move window to workspace
<ALT-SHIFT-[1-0]>                             Move window to workspace & switch

## Window layout
<SUPER-M>                                     Maximize window
<SUPER-SHIFT-P>                               Toggle horizontal/vertical window arrangement
<SUPER-SHIFT-F>                               Toggle floating
<SUPER-MOUSE-LEFT>                            Drag floating window
<SUPER-MOUSE-MIDDLE>                          Resize floating window
<SUPER-R>                                     Resize floating window using cursor or hjkl submap

## Workspaces
<SUPER-MOUSE-DOWN>                            Switch to next workspace
<SUPER-[1-0]>                                 Switch workspace
<SUPER-MOUSE-UP>                              Switch to previous workspace

## Device control
<FN-F1>                                       Mute
<FN-F2>                                       Decrease volume
<FN-F3>                                       Increase volume
<FN-F4>                                       Mute microphone
<FN-F5>                                       Decrease brightness
<FN-F6>                                       Increase brightness

## Screenshot
<PRTSC>                                       Screenshot whole screen
<SHIFT-PRTSC>                                 Screenshot selected area
<SUPER-PRTSC>                                 Screenshot active window

## Misc
<SUPER-SHIFT-C>                               Change wallpaper
<SUPER-SHIFT-R>                               Reload hyprland
<SUPER-V>                                     View clipboard

## rofi
<CTRL-TAB>                                    Toggle application / window mode
