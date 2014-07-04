Alt-Odroid U2/3 - Arch Linux - Mali/xorg-armsoc
===============================================

If you want to try the the latest Mali blob with dsd's xf86-video-armsoc as dicussed here :

http://forum.odroid.com/viewtopic.php?f=77&t=4456#p35809

I've built packages which do this.

**PKGBUILD's :** https://github.com/gripped/odroid-u2-pkgbuilds

**Packages :** http://odroidxu.leeharris.me.uk/u2/

To do this you can add a custom repo (as root) :


>cat >> /etc/pacman.conf <<EOF

>[odroidu]

>SigLevel = Never

>Server = http://odroidxu.leeharris.me.uk/u2

>EOF


And then update pacman :

>pacman -Syu

And then install them with pacman :

>pacman -S linux-odroidu-r4p0 mali-odroid-r4p0 xf86-video-armsoc-dsd xorg-server-dsd

And you'll need to edit /etc/xorg.conf. Mine now has


>\# X.Org X server configuration file for xfree86-video-mali
>
>Section "Device"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identifier "Mali-Fbdev"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Driver   "armsoc"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Option   "fbdev"           "/dev/fb1"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Option  "DriverName"      "exynos"

>

>EndSection

>

>Section "Screen"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identifier   "Mali-Screen"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Device       "Mali-Fbdev"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DefaultDepth 24 

>EndSection

>

>Section "DRI"

>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mode 0666

>EndSection


I'm not sure if I'm going to maintain/update these packages, etc as I don't know if I am going to keep using the armsoc driver myself. But the PKGBUILD's are there so you can fork the repo and DIY.
