# Installing linux on a NTFS partition
1) boot from a linux livecd which you want to install
2) open a console and run 3~10
3) sudo mount -o loop </path/to/image/file/name.img> /mnt
4) sudo unsquashfs -f -d /mnt </path/to/livecd/filesystem.squashfs>
5) sudo cp loop /mnt/usr/share/initramfs-tools/scripts/loop
6) sudo chroot /mnt
7) ln -sf boot/initrd.img-5.4.50-amd64-desktop initrd.img
8) ln -sf boot/vmlinuz-5.4.50-amd64-desktop vmlinuz
9) update-initramfs -u -k all
10) adduser --disabled-password --group sudo deepin

# Booting above system
1) place efi and grub directory in ESP partition
2) edit grub/grub.cfg
3) ...
