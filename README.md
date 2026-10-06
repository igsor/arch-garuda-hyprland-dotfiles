
# Basic System Setup

## Fix luks setup during installation
The calamares installer creates a luks configuration that is incompatible with GRUB's capabilities.
After the installer has finished but before the reboot you need to apply the following fix:
    cryptsetup luksChangeKey --pbkdf pbkdf2 /dev/nvme0n1p2
    cryptsetup luksChangeKey --pbkdf pbkdf2 /dev/nvme0n1p3

## Skip grub menu on startup
In `/etc/default/grub`, set GRUB_TIMEOUT to 0

## Enable autologin
In `/etc/sddm.conf`, in the "[Autologin]" section, add the line "User=<username>"

## Home cleanup
rmdir Public Templates Videos Projects Pictures

## Install common software
You might have installed some of those during the finalization of the installation (after first boot).
Otherwise, install them manually.

pacman -S neovim
pacman -S firefox
pacman -S okular
pacman -S scribus
pacman -S thunderbird

