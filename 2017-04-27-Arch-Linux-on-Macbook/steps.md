Followed https://medium.com/@philpl/arch-linux-running-on-my-macbook-2ea525ebefe3 up to "The rest of it".
Kept a 200GB Partition gap I plan to use for a docker native filesystem later.

Instead of putting kernel module names into ``/etc/modules`` as suggested in the howto, I create a file called ``/etc/modueles-load.d/macbook.conf`` and put them in there, which is more like it is suggested in "Automatic module handling" in https://wiki.archlinux.org/index.php/kernel_modules .

```
coretemp
applesmc
```

Sync the pacman package library:

```
pacman -Syyu
```

Install dhcpd, so that we have networking after the reboot.

```
pacman -S dhcpcd
systemctl enable dhcpcd
```

Set a password: ``passwd``

## Install a bootloader

```
pacman -S dosfstools
bootctl --path=/boot install
```

Save this into ``/boot/loader/entries/arch.conf``

```
title Arch Linux
linux /vmlinuz-linux
initrd /initramfs-linux.img
options root=/dev/sda2 rw elevator=deadline quiet splash resume=/dev/sda3 nmi_watchdog=0
```

make this the default boot entry

```
echo "default arch" > /boot/loader/loader.conf
```

Now we can boot into the system.

```
exit
reboot
```

Remove the usb drive!


# Installation

Following *Setting up Arch Linux* in https://medium.com/@philpl/arch-linux-running-on-my-macbook-2ea525ebefe3 to setup GNOME now.


```
groupadd users  # "users" group already existed for me
useradd -m -g users -G wheel -s /bin/bash stefanfoulis
pacman -S sudo
echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.s/wheel.conf
passwd stefanfoulis
passwd -l root
````


```
