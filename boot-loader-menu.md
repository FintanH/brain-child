---
title: Boot Loader Menu
date: 2020-11-29T14:09
tags: [operating-systems, nixos, learning, firmware]
---

Recently I had an issue with connecting my laptop to a new monitor. To be
honest, I still have the issue. My goal was to update my firmware using
`fwupdmgr`, but every time I would run it from the command line and restart it
would try do the same update again and again. So I took to the NixOS discourse
with a [post][nixos-post]. In that post I got an answer on how to get the
updates to persist and I also learned where those boot loader entries come from
on start-up!

When installing a Linux OS one of the last steps is mounting to the `/boot`
directory. I never really questioned what this even means. But if we run `tree`
on the directory it's a little bit enlightening:

```
$ tree -a /boot
/boot/
├── 405c7f4b907041528aaa214699e78dad
├── 67867db1890746a78758f3233980e0be
├── b74beca51d814050ae612611164f59a6
├── EFI
│   ├── arch
│   │   ├── fw
│   │   └── fwupdx64.efi
│   ├── BOOT
│   │   └── BOOTX64.EFI
│   ├── Linux
│   ├── nixos
│   │   ├── fw
│   │   │   ├── fwupd-4bbc40fa-f81e-4206-bc70-a1f7b744d964.cap
│   │   │   └── fwupd-f72e048b-65bd-4e71-9071-1ac7045223e5.cap
│   │   ├── fwupdx64.efi
│   │   ├── rlyz7g8dv4ydbrsmwf27n051inlmw7hp-initrd-linux-5.10-rc3-initrd.efi
│   │   └── sywq11dwgv92m2gppij9xkfqzjkhmmbb-linux-5.10-rc3-bzImage.efi
│   └── systemd
│       └── systemd-bootx64.efi
├── fbfa1febacce483cb3d7ba2a4c2ae554
├── FSCK0000.REC
├── initramfs-linux-fallback.img
├── initramfs-linux.img
├── initramfs-linux-lts-fallback.img
├── initramfs-linux-lts.img
├── intel-ucode.img
├── loader
│   ├── entries
│   │   ├── arch.conf
│   │   ├── nixos-generation-57.conf
│   │   ├── nixos-generation-58.conf
│   │   └── nixos-generation-59.conf
│   ├── loader.conf
│   └── random-seed
├── vmlinuz-linux
└── vmlinuz-linux-lts
```

There's some interesting entries under `EFI` and `loader/entries`. These
actually correspond to those items that show up at boot time!

So the aim of the game was to add an entry so that I could run the firmware
updater from the boot menu. This was simple enough. If I add a file called
`/boot/loader/entries/firmware_update.conf` with the following contents:

```
title          Linux Firmware Updater
efi            /EFI/nixos/fwupdx64.efi
```

then a new entry will greet me called `Linux Firmware Updater`. I could select
this and the firmware would get updated.

My quest to use my monitor continues, but at least I learned something new :)

[nixos-post]: https://discourse.nixos.org/t/x1-carbon-fwupdmgr-not-persisting/10128
