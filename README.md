 # way to add windows entry

First add this lines to `grub.cfg`

```shell
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 UEFI/GPT" {
		insmod part_gpt
		insmod fat
		insmod chain
		search --no-floppy --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

Then change `$hints_string` and `$fs_uuid`.

```shell
# find hints_string
# mount windows efi partation to /boot/efi
mount /dev/sdXn /boot/efi

# then run this command
grub-probe --target=hints_string esp/EFI/Microsoft/Boot/bootmgfw.efi


# find fs_uuid
lsblk -f
```
