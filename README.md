# Installing linux on a NTFS partition
1) sudo mount -o loop </path/to/image/file/name.img> /mnt
2) sudo unsquashfs -f -d /mnt </path/to/livecd/filesystem.squashfs>
3) sudo cp loop /mnt/usr/share/initramfs-tools/scripts/loop
4) sudo chroot /mnt
5) ln -sf boot/initrd.img-5.4.50-amd64-desktop initrd.img
6) ln -sf boot/vmlinuz-5.4.50-amd64-desktop vmlinuz
7) update-initramfs -u -k all
8) adduser --disabled-password --group sudo deepin

# Booting above system
1) place efi and grub directory in ESP partition
2) edit grub/grub.cfg
3) ...
