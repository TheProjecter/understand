#summary Running QNX Neutrino on QEMU
#labels QEMU,OMAP3,QNX,Neutrino,BeagleBoard,Momentics,Deprecated

## Installing QNX SDP On Linux Hosts ##
  * If you haven't already done so, [register](https://www.qnx.com/account/login.html#showcreate) for a QNX.com account, by following the instructions provided
  * Log-in to QNX.com using your account, and visit [this page](http://www.qnx.com/download/feature.html?programid=18773) to download a copy of QNX Software Development Platform 6.4.0 (includes both QNX Neutrino, and Momentics - a customised version of [Eclipse](http://www.eclipse.org)) for Linux
  * Set the Executable bit on the downloaded file (`qnxsdp-6.4.0-200810211530-linux.bin` as of writing) using `chmod +x qnxsdp-6.4.0-200810211530-linux.bin`
  * As root, or using `sudo`, run the downloaded file and follow the instructions provided, taking care to install the software to the default location of `/opt/qnx640`
  * Follow the remaining instructions and offers to install any additional software, if required
  * Once the process has completed, log-out of your desktop environment session, and log-on again
  * Follow the instructions [here](http://www.qnx.com/developers/articles/inst_3107_2.html) (from the "Activating QNX SDP 6.4.0" section) to enter any license keys and activate QNX Software Development Platform - free-of-cost license keys were provided for non-commercial/hobbyist use, last time I checked

## BeagleBoard Emulators and the QNX Board Support Package (BSP) ##
The [BeagleBoards](http://www.beagleboard.org) are based upon [Texas Instruments'](http://www.ti.com) OMAP-3530 CPUs using upon the ARM architecture, and QNX supply a basic [BSP](http://community.qnx.com/sf/wiki/do/viewPage/projects.bsp/wiki/TiOmap3530evm1.0.020080109ReleaseNotes?showDetails=true) for use with them. Unfortunately, the BSP far from "Just Works" with the emulated version of the BeagleBoard implemented in [QEMU-OMAP3](http://code.google.com/p/qemu-omap3).

## Useful Information ##
  * [The QNX Neutrino/SDP 6.4.0 Release Notes](http://www.qnx.com/developers/articles/rel_3101_16.html) contain a wealth of information related to using SDP, and errata to take note of