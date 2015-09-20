# What is QEMU? #
[QEMU](http://www.qemu.org) emulates a number of hardware platforms and CPU architectures (at least x86, ARM, MIPS and PowerPC), as well as a number of other devices (e.g. Secure Digital Card readers, Bluetooth radios, Ethernet chipsets, VGA adaptors, and audio chipsets).

# Variants and Forks #
  * [QEMU-OMAP3](http://code.google.com/p/qemu-omap3) concentrates on adding support for OMAP3 chipsets from Texas Instruments based upon the ARM architecture
  * The [Android Emulator](http://developer.android.com/guide/developing/tools/emulator.html) also emulates the ARM architecture and a custom chipset design (GoldFish)
  * Most of the patches necessary to run [Symbian OS](http://www.symbian.org) on QEMU have been accepted upstream by the QEMU developers, and the Syborg baseport is available [here](http://developer.symbian.org/oss/FCL/interim/QEMU)
  * Additional patches to support Python-based hardware devices, and the use of a host directory as a Symbian OS guest drive are hosted along with the baseport itself

# Operating Systems #

  * [QNX Neutrino](QNXNeutrinoOnQEMU.md)
  * [RISC OS](RISCOSOnQEMU.md)
  * [Symbian OS](CustomSyborgImages.md)