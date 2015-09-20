SVN/1.5.4 ([r33841](https://code.google.com/p/understand/source/detail?r=33841)) neon/0.28.3

https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2451 has HPUX nettl IGSSN and ICXGBE sample frames
https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2894 has Endace ERFII/Extension Header frames
## Controller-Area Network (CAN) on Linux ##
  * Assuming that you run a relatively recent Linux kernel (2.6.27 or higher?), there is a virtual CAN kernel module that can be enabled with `modprobe can can-raw vcan`
  * Assuming that the module exists, and was loaded, you should see `vcan: Virtual CAN interface driver` in the output of `dmesg`
  * Output from the other kernel modules should look like this:
`vcan: Virtual CAN interface driver`<br />`can: controller area network core (rev 20081130 abi 8)`<br />`NET: Registered protocol family 29`<br />`can: raw protocol (rev 20081130)`
> ip link add type vcan &&  ip link add dev can0 type vcan
    * Run `svn checkout svn://svn.berlios.de/socketcan/trunk socketcan` to check out a set of tools for working with Socket-CAN, and then run `cd socketcan/can-utils && make` to build them
    * Run `sudo ./vcan create` to create a new `vcan0` interface, and then `sudo ifconfig vcan0 up` to bring it up
    * If it worked, the output should look like this:

|`[tyson@nagasaki can-utils]$ sudo ifconfig vcan0`|
|:------------------------------------------------|
|`vcan0     Link encap:UNSPEC  HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00`|
|          `NOARP  MTU:16  Metric:1`              |
|          `RX packets:0 errors:0 dropped:0 overruns:0 frame:0`|
|        `TX packets:0 errors:0 dropped:0 overruns:0 carrier:0`|
|        `collisions:0 txqueuelen:0`              |
|        `RX bytes:0 (0.0 b)  TX bytes:0 (0.0 b)` |

## Temporary References ##

http://www.nabble.com/Can't-get-SocketCan-to-work-on-a-MPC5200b-board-td20467264.html
http://www.armadeus.com/wiki/index.php?title=CAN_bus_Linux_driver
http://openfacts.berlios.de/index-en.phtml?title=Socket-CAN
http://www.ethereal.com/lists/ethereal-users/200306/msg00256.html has a Niksun NetVCR ATM-over-T1 capture file (ATMoverT1Traffic.pcap)
http://www.ethereal.com/lists/ethereal-users/200212/msg00040.html has 2 Shomiti Snoop capture files
http://www.ethereal.com/lists/ethereal-dev/200404/msg00437.html
http://www.ethereal.com/lists/ethereal-users/200402/msg00146.html - Nokia libpcap with ATM/SDH packets
https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2401 might have WiMAX packets
https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2290 has GPRS-LLC with encrypted and unencrypted packets
https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=1688 - FireWall-1 capture
https://www.wireshark.org/lists/wireshark-dev/200611/msg00233.html - SNA VMStrace dump, won't open in WS though...

http://www.ethereal.com/lists/ethereal-dev/200303/msg00006.html - HP RBOOT
http://www.ethereal.com/lists/ethereal-dev/200308/msg00022.html - Endace ERF 1 (ATM, Ethernet, Cisco HDLC)
http://www.ethereal.com/lists/ethereal-dev/200308/msg00399.html - Endace ERF 2 (Ethernet, ATM, POS CHDLC, POS PPP)

## Iterasi packages ##
FireFox add-on stores working data inside $HOME/Library/Caches/TemporaryItems/iterasi/{5-part GUID} as a loose collection of objects related to a page (e.g. PNG/GIF/JPEG image files and CSS documents), as well as a thumbnail.jpg file, an Asset.xml file and a {5-part GUID}-Document.txt file. Naming conventions are {5-part GUID}-Style{1-indeterminate number}.css for stylesheets, {5-part GUID}-Default.html for the main document, and {5-part GUID}-Asset{1-indeterminate number}.{file name extension} for all others.
It seems that the main document is compressed and encrypted using an unknown set of algorithms, according to Asset.xml - presumably to obfuscate the content of it.

OpenSolaris Extended Attributes
root@opensolaris:~# runat .
shell-init: error retrieving current directory: getcwd: cannot access parent directories: No such file or directory
root@opensolaris:~# ls
SUNWattr\_ro  SUNWattr\_rw
root@opensolaris:~# file **SUNWattr\_ro:	unix-rt ldp
SUNWattr\_rw:	unix-rt ldp**

Not possible to store directories in namespace

root@opensolaris:~# /etc/tar c@v/f SolarisMetadata.tar SolarisMetadata
a SolarisMetadata/ 0K
a SolarisMetadata attribute . 0K
a SolarisMetadata attribute ANewAttribute 1K
a SolarisMetadata attribute copy-SUNWattr\_ro 1K
a SolarisMetadata attribute copy-SUNWattr\_rw 1K

Potential method for archiving Doors
> find /var/run/name\_service\_door /var/run/SolarisMetadata  -depth -print | cpio -oP@v

find /var/run/name\_service\_door /var/run/SolarisMetadata  -depth -print | cpio -oP@v >  ~/CPIO-Test
/var/run/name\_service\_door
/var/run/SolarisMetadata/rcm\_daemon\_door
/var/run/SolarisMetadata/SolarisFIFO
/var/run/SolarisMetadata/file
/var/run/SolarisMetadata/file attribute .
/var/run/SolarisMetadata/file attribute AnotherOne
/var/run/SolarisMetadata
8 blocks

Vista/7 UDF:
sudo mount /dev/scd1 /media/cdrom1 -s -t udf -o ro,user,noauto,exec,umask=0,session=0
> dvd+rw-mediainfo /dev/dvd
> wodim dev='/dev/sr1' -toc
> sudo mount /dev/scd1 /media/cdrom1 -s -t udf -o ro,user,noauto,exec,umask=0,session=0,lastblock=266636
format x: /fs:UDF
http://serverfault.com/questions/55089/with-what-tool-should-i-format-a-hard-drive-as-udf