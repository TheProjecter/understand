﻿#summary Running RISC OS on QEMU
#labels RISC\_OS,QEMU,OMAP3,BeagleBoard

# RISC OS on QEMU-OMAP3 #
If you prefer, there is a pre-patched version of [QEMU-OMAP3](http://code.google.com/p/qemu-omap3) [here](http://understand.googlecode.com/files/qemu-omap3-risc_os.tar.bz2). Additional information and tools that may be useful are available [here](http://www.riscosopen.org/wiki/documentation/pages/Cortex-A8+port).

Whilst writing this, I stored all related files in `$HOME/RISC_OS`, and most paths mentioned are absolute or relative, based upon that directory. I suggest that you use the same directory, or another suitable one.

Thanks to the kind folks in the `#riscos` IRC channel on <a href='http://www.freenode.org'> FreeNode</a> for their assistance and persistence during this undertaking, and for coping with any misunderstandings or issues I had.

  * Otherwise, download the patch from [here](http://understand.googlecode.com/files/qemu-omap3-patch.txt), as well as the QEMU-OMAP3 [tarball](http://qemu-omap3.googlecode.com/files/qemu-omap3-v0.01.tar.bz2)
  * Unpack the QEMU-OMAP3 tarball in the usual manner (`bunzip2 qemu-omap3-v0.01.tar.bz2 && tar xvf qemu-omap3-v0.01.tar`)
  * Apply the patch with `patch < qemu-omap3-patch.txt`, taking care to choose the `+++ qemu-omap3/` files, over the `--- qemu-omap3-orig/` ones
  * Ensure that a GCC 3.4.x release is installed, or install one from your Linux distribution's repositories (assuming you use a Linux distribution)
  * For speed, run `./configure --target-list=arm-softmmu && make` to build only the ARM emulator target
  * If everything went to plan, you should have these binaries and scripts in the QEMU-OMAP3 patched source directory:
| `bb_nandflash_ecc` | `bb_nandflash.sh`| `dyngen` | `qemu-img` | `qemu-nbd` |
|:-------------------|:-----------------|:---------|:-----------|:-----------|

  * There should also be a `qemu-system-arm` binary in the `arm-softmmu` subdirectory
  * Download and unzip the BeagleBoard ROM archive from [here](http://www.riscosopen.org/zipfiles/misc/rom-omap.5.15.zip?1249001397) - this may be superseded by later versions listed on [this](http://www.riscosopen.org/content/downloads/other-zipfiles) page
  * Obtain the UBoot 1.3.3 and XLoader 1.41 test image from [here](http://qemu-omap3.googlecode.com/files/image-v0.01.tar.bz2), extract the contents using `bzip2` and `tar`, and discard or move the `uImage` file elsewhere (it contains a Linux kernel)
  * Rename the extracted `OMAP3Dev` ROM image file from `rom-omap.5.15.zip` to `riscos.rom`

For the avoidance of any doubt, or any confusion, there is **not** a `beagle-nand.bin` file shipped with QEMU-OMAP3 (this is generated manually) from the files extracted from `image-v0.01.tar.bz2`.

  * Run `./qemu-omap3-risc_os/bb_nandflash.sh x-load.bin.ift beagle-nand.bin x-loader` and wait a little while, to be presented with this:

`flash image name:beagle-nand.bin`<br />
`beagle-nand.bin does not exist.Create it!`<br /><br />
`xloader image name:x-load.bin.ift`<br />`1+0 records in`<br />`0+1 records out`<br />`2048 bytes (2.0 kB) copied, 0.0505243 s, 40.5 kB/s`<br />`1+0 records in`<br />`0+1 records out`<br />`2048 bytes (2.0 kB) copied, 0.0323682 s, 63.3 kB/s`<br />`1+0 records in`<br />`0+1 records out`<br />`2048 bytes (2.0 kB) copied, 8.8908e-05 s, 23.0 MB/s`<br />`1+0 records in`<br />`0+1 records out`<br />`2048 bytes (2.0 kB) copied, 0.0148137 s, 138 kB/s`<br />`0+1 records in`<br />
`0+1 records out`<br />`8 bytes (8 B) copied, 0.000108463 s, 73.8 kB/s`<br />`put xloader into flash image done!`<br />

  * Now run `./qemu-omap3-risc_os/bb_nandflash.sh riscos.rom beagle-nand.bin u-boot` to receive some more (very similar) copying messages
  * Finally, to complete the home stretch, run `./qemu-omap3-risc_os/bb_nandflash_ecc beagle-nand.bin 0x0 0xe80000`, to receive a nice, shiny 256MB file named beagle-nand.bin
  * To test, run `./qemu-omap3-risc_os/arm-softmmu/qemu-system-arm -M beagle -m 256  -mtdblock ./beagle-nand.bin`, hit Ctrl+2 and bask in the glow of `serial0 console`<br />`Texas Instruments X-Loader 1.41`<br />`Starting OS bootloader...`,<br />` A0012345612123BCDBCEFGDSS init`<br /> from the RISC OS kernel and bootloader, as well as [this](http://paster.dazjorz.com/?p=4416) in the shell - sadly, thanks to broken USB support, it gets stuck there indefinitely

## Attempting to run a bare RISC OS ROM image on QEMU-OMAP3, without patches ##
Take heed that the BeagleBoard and most ARM-based devices emulated by QEMU-OMAP3 only support a maximum of 256MB of RAM.

If you didn't patch QEMU-OMAP3, expect results similar to these. If you're lucky, you might also see a window filled with a white framebuffer screen:

`[tyson@nagasaki ~]$ ./qemu-omap3/arm-softmmu/qemu-system-arm -M beagle  -kernel riscos  -m 256`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`gptimer ckl 8000`<br />`Segmentation fault`


If you used `./qemu-omap3/arm-softmmu/qemu-system-arm -M n800 -kernel riscos -m 256` instead, you'll get the same `gptimer ckl 8000` spray, but with this little extra:

`f->base 0 f->size 1000000`<br />`mipid_reset: Display off`<br />`f->base 4000000 f->size 1000000`<br />`Unassigned mem writeb 49020000 = 0x41 pc 80010064`<br />

## Screenshots of RISC OS on QEMU ##
<a href='http://picasaweb.google.com/lh/photo/c9sQrKtw8Hy4KUIU-B3LfQ?feat=embedwebsite'><img src='http://lh5.ggpht.com/_Y5mZY1-de8o/SjJ25da9wzI/AAAAAAAAB2k/gs4XqH5oWZE/s144/serial_console_1.png' /></a>

## Additional Information ##
  * [This page](https://www.riscosopen.org/wiki/documentation/pages/Using+the+Cortex-A8+port) on the RISC OS Open Wiki has slightly more up-to-date information regarding building RISC OS images for QEMU.