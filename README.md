# Installing linux on a NTFS partition
1) boot from a linux livecd which you want to install
2) open a console and run
```
sudo mount -o loop /path/to/image/file/name.img /mnt
sudo unsquashfs -f -d /mnt /path/to/livecd/filesystem.squashfs
sudo cp loop /mnt/usr/share/initramfs-tools/scripts/loop
sudo chroot /mnt
ln -sf boot/initrd.img-$(uname -r) initrd.img
ln -sf boot/vmlinuz-$(uname -r) vmlinuz
update-initramfs -u -k all
adduser --disabled-password --group sudo deepin
```

# Booting system
1) place efi and grub directory in ESP partition
2) edit grub/grub.cfg
```
menuentry 'Windows' {
	set img_file=/efi/Microsoft/Boot/bootmgfw.efi
	search --file --set=img_dev --no-floppy $img_file
	set root=($img_dev)
	chainloader $img_file
}
menuentry 'Linux' {
        set img_file=/path/to/image/file/name.img
        search --file --set=img_dev --no-floppy $img_file
        probe --set part_uuid --fs-uuid ($img_dev)
        loopback loop ($img_dev)$img_file
        linux (loop)/vmlinuz boot=loop root=UUID=$part_uuid loop=$img_file rw intel_iommu=on pcie_acs_override=downstream,multifunction i915.enable_gvt=1 kvm.ignore_msrs=1 nouveau.modeset=0 vfio_iommu_type1.allow_unsafe_interrupts=1 vfio-pci.ids=10de:1d10,10de:1ba1,10de:10f0,10de:1f11,10de:10f9,10de:1ada,10de:1adb video=vesafb:off,efifb:off
        initrd (loop)/initrd.img
}
```
3) ...
