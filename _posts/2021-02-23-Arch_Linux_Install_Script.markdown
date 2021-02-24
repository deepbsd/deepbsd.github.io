---
layout: post
title: Arch Linux Install Script
date: 2021-02-23 21:58:29-05:00
categories: Linux Arch
---

# Arch Linux Install Script

Many new Linux users eventually gravitate toward a more minimal Linux distro where they
essentially get to build their own distro, according to their own preferences rather
than Canonical's or another big distro sponsor.  Arch Linux is a terrific destination
for these intermediate Linux users, because there is a lot of freedom and choice.  You
get to build your own distro, since you install it by hand.  After you've installed Arch
by hand a few times, you'll probably want to create your own Arch install script.  

Since you've already installed the distro by hand several times, you probably already have
a list of preferred applications and ways of installing Arch.  This script will reflect
the simplest possible steps that are automated yet easily comprehended by someone not
totally brand new to bash scripting.

This script, named `simplest.sh`, is mainly a skeleton that you can modify and that can
grow with your growing scripting skills.  WARNING: I'm using an MBR disk label here.  This 
will probably not work with a UEFI Motherboard or EFI bios.  For that you should really
use a GPT disk label with an EFI partition formatted with FAT-32.  My other install scripts
use this format, or they are capable of branching to install with GPT disk label and EFI 
partitioning scheme according to whether a fully compliant EFI bios exists.  I'll revisit
this later.

Here's my `simplest.sh` script, which should just give you a starting place for your own
script.  This script does not install X.  You can have that as a future exercise!

```
 1	#!/usr/bin/env bash
   
 2	##  This is the simplest possible Arch Linux install script I think...
 3	HOSTNAME="marbie1"
 4	#VIDEO_DRIVER="xf86-video-vmware"
 5	IN_DEVICE=/dev/sda
 6	BOOT_DEVICE="${IN_DEVICE}1"
 7	ROOT_DEVICE="${IN_DEVICE}2"
 8	SWAP_DEVICE="${IN_DEVICE}3"
 9	HOME_DEVICE="${IN_DEVICE}4"
   
10	BOOT_SIZE=512M
11	SWAP_SIZE=2G
12	ROOT_SIZE=13G
13	HOME_SIZE=    # Take whatever is left over after other partitions
14	TIME_ZONE="America/New_York"
15	LOCALE="en_US.UTF-8"
16	#KEYBOARD="us"    # change if you need to
17	FILESYSTEM=ext4
   
18	use_bcm4360(){ return 1; }  # return 0 for "truthy" and 1 for "falsy"
   
19	if $(use_bcm4360) ; then
20	    WIRELESSDRIVERS="broadcom-wl-dkms"
21	else
22	    WIRELESSDRIVERS=""
23	fi
   
24	BASE_SYSTEM=( base base-devel linux linux-headers linux-firmware dkms vim iwd )
   
25	devel_stuff=( git nodejs npm npm-check-updates ruby )
26	printing_stuff=( system-config-printer foomatic-db foomatic-db-engine gutenprint cups cups-pdf cups-filters cups-pk-helper ghostscript gsfonts )
27	multimedia_stuff=( brasero sox cheese eog shotwell imagemagick sox cmus mpg123 alsa-utils cheese )
   
28	# VERIFY BOOT MODE
29	efi_boot_mode(){
30	    [[ -d /sys/firmware/efi/efivars ]] && return 0
31	    return 1
32	}
   
33	# All purpose error
34	error(){ echo "Error: $1" && exit 1; }
   
35	###############################
36	###  START SCRIPT HERE
37	###############################
   
38	### Check of reflector is done
39	clear
40	echo "Waiting until reflector has finished updating mirrorlist..."
41	while true; do
42	    pgrep -x reflector &>/dev/null || break
43	    echo -n '.'
44	    sleep 2
45	done
   
46	### Test internet connection
47	clear
48	echo "Testing internet connection..."
49	$(ping -c 3 archlinux.org &>/dev/null) || (echo "Not Connected to Network!!!" && exit 1)
50	echo "Good!  We're connected!!!" && sleep 3
   
51	## Check time and date before installation
52	timedatectl set-ntp true
53	echo && echo "Date/Time service Status is . . . "
54	timedatectl status
55	sleep 4
   
56	$(efi_boot_mode) && error "You have a UEFI Bios; Please use the Farchi or Darchi script for installation"
   
57	####  Could just use cfdisk to partition drive
58	#cfdisk "$IN_DEVICE"    # for non-EFI VM: /boot 512M; / 13G; Swap 2G; Home Remainder
   
59	###  NOTE: Drive partitioning is one of those highly customizable areas where your
60	###        personal preferences and needs will dictate your choices.  Many options
61	###        exist here.  An MBR disklabel is very old, limited, and may well inspire
62	###        you to investigate other options, which is a good exercise.  But, MBR is pretty
63	###        simple and reliable, within its constraints.  Bon voyage!
   
   
   
64	# Using sfdisk because we're talking MBR disktable now...
65	cat > /tmp/sfdisk.cmd << EOF
66	$BOOT_DEVICE : start= 2048, size=+$BOOT_SIZE, type=83, bootable
67	$ROOT_DEVICE : size=+$ROOT_SIZE, type=83
68	$SWAP_DEVICE : size=+$SWAP_SIZE, type=82
69	$HOME_DEVICE : type=83
70	EOF
   
71	sfdisk "$IN_DEVICE" < /tmp/sfdisk.cmd 
   
72	#####  Format filesystems
73	mkfs.ext4 "$BOOT_DEVICE"    # /boot
74	mkfs.ext4 "$ROOT_DEVICE"    # /
75	mkswap "$SWAP_DEVICE"       # swap partition
76	mkfs.ext4 "$HOME_DEVICE"    # /home
   
77	#### Mount filesystems
78	mount "$ROOT_DEVICE" /mnt
79	mkdir /mnt/boot && mount "$BOOT_DEVICE" /mnt/boot
80	swapon "$SWAP_DEVICE"
81	mkdir /mnt/home && mount "$HOME_DEVICE" /mnt/home
   
82	lsblk && echo "Here're your new block devices. (Type any key to continue...)" ; read empty
   
   
83	###  Install base system
84	clear
85	echo && echo "Press any key to continue to install BASE SYSTEM..."; read empty
86	pacstrap /mnt "${BASE_SYSTEM[@]}"
87	echo && echo "Base system installed.  Press any key to continue..."; read empty
   
88	# GENERATE FSTAB
89	echo "Generating fstab..."
90	genfstab -U /mnt >> /mnt/etc/fstab
91	cat /mnt/etc/fstab
92	echo && echo "Here's your fstab. Type any key to continue..."; read empty
   
93	## SET UP TIMEZONE AND LOCALE
94	clear
95	echo && echo "setting timezone to $TIME_ZONE..."
96	arch-chroot /mnt ln -sf /usr/share/zoneinfo/"$TIME_ZONE" /etc/localtime
97	arch-chroot /mnt hwclock --systohc --utc
98	arch-chroot /mnt date
99	echo && echo "Here's the date info, hit any key to continue..."; read empty
   
100	## SET UP LOCALE
101	clear
102	echo && echo "setting locale to $LOCALE ..."
103	arch-chroot /mnt sed -i "s/#$LOCALE/$LOCALE/g" /etc/locale.gen
104	arch-chroot /mnt locale-gen
105	echo "LANG=$LOCALE" > /mnt/etc/locale.conf
106	export LANG="$LOCALE"
107	cat /mnt/etc/locale.conf
108	echo && echo "Here's your /mnt/etc/locale.conf. Type any key to continue."; read empty
   
109	## HOSTNAME
110	clear
111	echo && echo "Setting hostname..."; sleep 3
112	echo "$HOSTNAME" > /mnt/etc/hostname
   
113	cat > /mnt/etc/hosts <<HOSTS
114	127.0.0.1      localhost
115	::1            localhost
116	127.0.1.1      $HOSTNAME.localdomain     $HOSTNAME
117	HOSTS
   
118	echo && echo "/etc/hostname and /etc/hosts files configured..."
119	echo "/etc/hostname . . . "
120	cat /mnt/etc/hostname 
121	echo "/etc/hosts . . ."
122	cat /mnt/etc/hosts
123	echo && echo "Here are /etc/hostname and /etc/hosts. Type any key to continue "; read empty
   
124	## SET ROOT PASSWD
125	clear
126	echo "Setting ROOT password..."
127	arch-chroot /mnt passwd
   
128	## INSTALLING MORE ESSENTIALS
129	clear
130	echo && echo "Enabling dhcpcd, pambase, sshd and NetworkManager services..." && echo
131	arch-chroot /mnt pacman -S git openssh networkmanager dhcpcd man-db man-pages pambase
132	arch-chroot /mnt systemctl enable dhcpcd.service
133	arch-chroot /mnt systemctl enable sshd.service
134	arch-chroot /mnt systemctl enable NetworkManager.service
135	arch-chroot /mnt systemctl enable systemd-homed
136	echo && echo "Press any key to continue..."; read empty
   
137	## ADD USER ACCT
138	clear
139	echo && echo "Adding sudo + user acct..."
140	sleep 2
141	arch-chroot /mnt pacman -S sudo bash-completion sshpass
142	arch-chroot /mnt sed -i 's/# %wheel/%wheel/g' /etc/sudoers
143	arch-chroot /mnt sed -i 's/%wheel ALL=(ALL) NOPASSWD: ALL/# %wheel ALL=(ALL) NOPASSWD: ALL/g' /etc/sudoers
144	echo && echo "Please provide a username: "; read sudo_user
145	echo && echo "Creating $sudo_user and adding $sudo_user to sudoers..."
146	arch-chroot /mnt useradd -m -G wheel "$sudo_user"
147	echo && echo "Password for $sudo_user?"
148	arch-chroot /mnt passwd "$sudo_user"
   
149	## INSTALL WIFI
150	$(use_bcm4360) && arch-chroot /mnt pacman -S "$WIRELESSDRIVERS"
151	[[ "$?" -eq 0 ]] && echo "Wifi Driver successfully installed!"; sleep 5
   
152	## Not installing X in this script...
   
153	## INSTALL GRUB
154	clear
155	echo "Installing grub..." && sleep 4
156	arch-chroot /mnt pacman -S grub os-prober
   
157	## We're not checking for EFI; We're assuming MBR
158	arch-chroot /mnt grub-install "$IN_DEVICE"
   
159	echo "configuring /boot/grub/grub.cfg..."
160	arch-chroot /mnt grub-mkconfig -o /boot/grub/grub.cfg
161	[[ "$?" -eq 0 ]] && echo "mbr bootloader installed..."
   
162	echo "Your system is installed.  Type shutdown -h now to shutdown system and remove bootable media, then restart"
163	read empty

```

## Notes About Simplest.sh

As I mentioned, I'm using an MBR disk label.  You'll want to change this if you're installing
to a newer motherboard or BIOS.  


