
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


