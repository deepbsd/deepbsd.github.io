---
layout: post
title: Migrating Antergos to Arch Linux
date: 2019-11-01 11:23:07-04:00
categories: linux arch antergos
---

## Note: This is just a beginning draft...

# Migrating Antergos Linux to Arch Linux

Since the Antergos project eneded, those of us who have loved Antergos have been sad. 

And there was Antergos forum post about future updates magically updating or migrating
Antergos installations to Arch Linux installations.  Well, that may not have happened to so
magically, and I guess no one every really promised us Linux magic, especially with an Arch
related distro, so we have to spin up our own magic I guess.  Hopefully, this article can
provide a bit of that.

I'm writing this on the first day of November, 2019, and the project ended in late May.  So there have
been updates that have helped to change existing Antergos installations into Almost Arch installations.
But there are a few things that still need to happen. Here's a recipe for converting your
Antergos installation into a working Arch installation:

1. Change to multi-user (non-graphical) run level.
    ```
    # systemctl start multi-user.target
    ```
2. Remove the pamac graphical package manager.
    ```
    # kill -s SIGKILL $(pgrep pamac) && pacman -R pamac
    ```
3. Remove all antergos packages (if you want a pure Arch installation).
    ```
    # pacman -Rddnus $(pacman -Qq | grep antergos)
    ```
4. Modify /etc/pacman.conf to remove references to Antergos repos.
Just comment out all sections with `[antergos]` or `[antergos-staging]`

5. Change entries in /etc/os-release (which is a symlink /usr/lib/os-release) over to Arch values
    ```
    NAME="Arch Linux"
    PRETTY_NAME="Arch Linux"
    ID=archlinux
    ID_LIKE=archlinux
    ANSI_COLOR="0;36"
    HOME_URL="https://archlinux.org/"
    SUPPORT_URL="https://bbs.archlinux.org/"
    BUG_REPORT_URL="https://bugs.archlinux.org"
    ```

6. Update your system: 
    ```
    pacman -Syyu
    ```

7. Make sure you have all required files for your desktop environment, including all Xorg and related
   files, video drivers, mesa, etc etc, which are now coming from Arch repos.  May need to
   re-install from new repos.



8. Change grub theme to an arch linux theme, if that's what you want. Remove Antergos grub
   theme.  Might need to update /etc/default/grub.cfg.
9. Restart your graphical target run level.
10. Reboot your computer, if you dare!






