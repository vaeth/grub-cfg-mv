# grub-cfg-mv

(C) Martin Väth (martin at mvath.de).
This project is under the GPL-2 license.
SPDX-License-Identifier: GPL-2.0-only

A grub.cfg library/example for __GRUB2__

The generator tool `grub-mkconfig` provided by GNU's __GRUB2__ bootloader
is far from being optimal for many purposes.

It can be very hard to modify that generator tool to produce a reasonable
configurable menu. Instead of modifying this script, I recommend
to write the desired config directly into your `boot/grub/grub.cfg`
and to load a "library" of convenient functions to use from your config.

The provided `boot/grub/grub-mv.cfg` is such a library.
It should be mostly self-explanatory, especially when you see how
it is used in the provided `boot/grub/grub.cfg`.

The latter assumes that there are two _ext4_ partitions (`sda1` and `sda2`)
and a further _swap_ (suspend) partition (`sda3`), all on the first harddisk
with an _msdos_ partition table, the first two partitions containing
two linux installations (one for 64 bit and one for 32 bit).
The files `/boot/bzImage`, `/boot/bzImage.previous` and `/boot/bzImage.debug`
are supposed to be symlinks to the current/previous/debugging kernel
of the corresponding partition.
If you compile/install the kernels with https://github.com/vaeth/kernel
these symlinks will be updated automatically.

No initramfs is supposed to be used - with the exception of
`/boot/intel-uc.img` so that the kernel can update
your processors microcode before starting (recommended).

Read the grub documentation if you need initramfs for another purpose
or other fancy configuration stuff.

In the example configuration also some further tools (__SMB boot manager__
and __memtest__) are supposed to be installed.

Of course, it is not really expected that this is your partition layout:
This is merily an example, and should be easy to modify.
However, even if by accident you should have exactly the same layout,
you have to modify the provided grub.cfg to set appropriate values
for `PARTUUID` and `UUID`.
