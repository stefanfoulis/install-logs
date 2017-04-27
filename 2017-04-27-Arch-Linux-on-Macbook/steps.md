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
