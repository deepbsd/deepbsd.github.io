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
   re-install from new repos.  One of my machines had Cinnamon (desktop) antergos repos, so I
   had to remove all of those and get regular arch packages.  Just to be safe, I re-installed
   all my xorg packages along with lightdm packages and my video drivers.  This time I knew
   they all came from arch repos.  
   [This article](https://www.tecmint.com/install-cinnamon-desktop-in-arch-linux)
   explains the process for Cinnamon. This particular article is good, but it is old (2014).
   Packages names can change a lot!

8. Change grub theme to an arch linux theme, if that's what you want. Remove Antergos grub
   theme.  (Should already be gone.) When you install grub from arch repos, it may not
   overwrite your existing antergos ```/etc/default/grub.cfg```.  If not, there should be
   another grub.cfg in /etc/default that has a different name, like grub.cfg.pacman or
   something.  Look at them both and make sure the correct one is in ```/etc/default/grub.cfg```.
   I would also install a grub theme, such as ```grub2-theme-archlinux```
   ```
   # yay -S grub2-theme-archlinux
   ```
   Then, run
   ```
   # grub-mkconfig -o /boot/grub/grub.cfg
   ```
   If there are no errors, you should be good for a reboot, almost. 
9. Restart your graphical target run level.
   ```
   # systemctl start graphical.target
   ```
   If there are any missing X related packages, you can troubleshoot your errors and
   straighten them out.
10. When youre ready, reboot your computer, if you dare!

# Leftovers

If you installed Antergos using LVM, you'll still see `Antergos` in your LVM names.  There
are still some packages on your system, such as webkit-theme-antergos, and you can see some
more using ```updatedb && locate antergos```.  But for all intents and purposes, you now
should have an arch linux installation.  Those remaining files can be removed manually I
think without affecting the rest of the system.  But I'm not sure.  For now, they're not
bothering me.  Maybe I'll remove them later.

I've changed my icons around to reflect the change, in my start menu for example.  Neofetch
and Screenfetch now report an Arch installation.  And really, there's just very little left
of Antergos in the installation.  Linux distros are simply a collection of choices, and
Antergos was mainly a collection of very nice styling decisions and special packages, and
those packages are now replaced by Arch packages.  And you're free to keep the best choices
for your indidualized Arch installation!




