# Installing linux on a NTFS partition
sudo mount -o loop </path/to/image/file/name.img> /mnt
sudo unsquashfs -f -d /mnt </path/to/livecd/filesystem.squashfs>
sudo cp loop /mnt/usr/share/initramfs-tools/scripts/loop
sudo chroot /mnt
ln -sf boot/initrd.img-5.4.50-amd64-desktop initrd.img
ln -sf boot/vmlinuz-5.4.50-amd64-desktop vmlinuz
update-initramfs -u -k all
adduser --disabled-password --group sudo deepin

# Booting above system
1) place efi and grub directory in ESP partition
2) edit grub/grub.cfg
3) ...
