## General Overview ##

The BT Home Hub contains a 32-bit, MIPS architecture, Broadcom BCM6348KPBG/BCM6348 CPU, supporting ADSL2. Running the UNIX/Linux `file` command on one of the binaries extracted from the router reported "`ELF 32-bit MSB executable, MIPS, version 1 (SYSV)`". A Linux kernel is used on the device, however a closed-source, proprietary userland application (`linux_appl.exe`) and a closed-source, proprietary kernel module (`nmon.ko`) are responsible for providing the Home Hub's functionality.

Despite being BT-branded, it appears that several organisations (or related subsidiaries of them) have played a part in designing the hardware and software in this device. The MAC address of a typical Home Hub is reported as being within the range assigned to Thomson by Wireshark, and Alcatel and InvenTel are also mentioned in places throughout the firmware.

## Telnet Header for Firmware 6.1.1.R ##
<img src='http://understand.googlecode.com/svn/wiki/HubHeader.png' />

## Output of System Commands (Telnet) ##
  * The output of `debug exec dmesg` can be seen, [here](http://understand.googlecode.com/svn/wiki/BTHomeHub-debug-exec-dmesg.txt)