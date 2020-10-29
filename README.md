# Installing linux on a NTFS partition
1) boot from a linux livecd which you want to install
2) open a console and run
```
sudo mount -o loop </path/to/image/file/name.img> /mnt
sudo unsquashfs -f -d /mnt </path/to/livecd/filesystem.squashfs>
sudo cp loop /mnt/usr/share/initramfs-tools/scripts/loop
sudo chroot /mnt
ln -sf boot/initrd.img-$(uname -r) initrd.img
ln -sf boot/vmlinuz-$(uname -r) vmlinuz
update-initramfs -u -k all
adduser --disabled-password --group sudo deepin
```

# Booting above system
1) place efi and grub directory in ESP partition
2) edit grub/grub.cfg
3) ...
