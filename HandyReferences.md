## Additional Sources of Packet Captures ##
  * A number of BACnet packet captures are available [here](http://kargs.net/captures/)
  * The [pcapr.net](http://pcapr.net) service provides an open-access capture file repository, facilities for uploading new files and a number of other tools
  * The [Sample Captures](http://wiki.wireshark.org/SampleCaptures) page on the [Wireshark Wiki](http://wiki.wireshark.org) is a useful source of protocol capture files
  * A trove of obscure, unique, old, and new capture files that have been used in the development and testing of [Wireshark](http://www.wireshark.org) is available in the form of the [Wireshark Mailing Lists](http://www.wireshark.org/lists/)
  * Even more sample files are available on the old [Ethereal Mailing Lists](http://www.ethereal.com/lists/), although they may disappear in the future - archiving those files here, or on the new Wireshark Wiki might be a good idea
  * The [Wireshark Bugzilla](https://bugs.wireshark.org) instance is also another good source of capture files
  * [Packet Life](http://packetlife.net/captures/) have various user-submitted capture files, as well as forums and a number of other resources
  * The page [here](http://aa-security.de/dumps/) has some capture files of historical interest (containing 3Com XNS, Token Ring, NetBIOS, IPX, ISDN and FDDI packets, amongst others)
  * [This page](http://www.thetechfirm.com/packets/index.html) has samples of various protocols, and notes on differences between analyser dissector implementations
  * An annotated trace of an iTunes 7 DAAP session is available, [here](http://www.webpages.ttu.edu/mroth/tunes/login.htm)
  * A capture file containing SocketCAN frames is [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4299)
  * The page [here](http://jon.oberheide.org/uverse/) has some AT&T U-Verse packet captures
  * Microsoft have released a number of capture files, to accompany their "open" documentation [here](http://sysdoccap.codeplex.com/wikipage?title=System%20Overview%20Document%20Scenario%20Captures)
  * A trace containing [TeraBeam TurboCell](http://www.terabeam.com/solutions/network_opt/turbocell.php) 802.11 frames is available [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2399)
  * A number of storage protocol-related traces are available [here](http://www.nlabooks.com/Resources.htm)

## Specification Documents and Useful Information ##
  * Internet Drafts from the [Internet Engineering Task Force (IETF)](http://www.ietf.org) are available [here](http://www.ietf.org/ID.html)
  * Requests For Comments (RFC) documents from the IETF are available [here](http://www.ietf.org/rfc.html)
  * The [Optical Storage Technology Association (OSTA)](http://www.osta.org) Universal Disk Format (UDF) specifications are available [here](http://osta.org/specs/index.htm)
  * A number of specifications covered under the [Microsoft Open Specification Promise](http://www.microsoft.com/interop/osp/default.mspx) are available [here](http://msdn.microsoft.com/en-us/library/cc203350.aspx)
  * A copy of the [VINES Protocol Definition](http://banyan.bamertal.com/Banyan-supplier-help/ProtoDef/ProtoDefMain.htm) is available
  * A header file containing a list of libpcap/tcpdump DLT values is available [here](http://fxr.watson.org/fxr/source/net/bpf.h) (although it may not be up-to-date)
  * [This blog post](http://taosecurity.blogspot.com/2006/01/freebsd-networking-over-firewire-you.html) contains a `tshark` text dump of an Apple IP-over-1394 packet that can be converted to a usable packet capture file with `text2pcap -l 138 `after saving it to a file
  * The Unified EFI (UEFI) 2.3 specifications, which include additional information on the GUID Partition Table (GPT) in chapter 5 are available [here](http://www.uefi.org/specs/), after registration
  * The Plan9 IL protocol specifications are available, [here](http://doc.cat-v.org/plan_9/4th_edition/papers/il/)
  * DECnet Phase IV protocol specifications are available, [here](http://linux-decnet.sourceforge.net/docs/doc_index.html)

## Protocol Stack Implementations ##
  * An implementation of FlexRay for Linux is available, [here](http://scriptkiller.de/en/a37/computer_electronics/linux/flexray_4_linux/flexray_protocol_stack_for_linux/)
  * An implementation of Media-Oriented Systems Transport (MoST) for Linux is available, [here](http://most4linux.sourceforge.net/)
  * Microsoft's raw NetBIOS implementation from Windows XP is available, [here](http://www.mac-net.com/174984.page)
  * LANtastic 8.01 (works as a 45 day trial, without a license) is available, [here](http://pcmicro.com/lantastic)
  * An implementation of AX.25 and a number of other amateur radio-related protocols, as well as links to protocol documentation is available, [here](http://www.linux-ax25.org)

## Tools ##
  * [Wireshark](http://www.wireshark.org) is probably the best (Open Source) protocol analyser and network monitor - no introduction is really necessary
    * A dissector for the QNX QNET protocol is available, [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3934)
  * Until someone can add support for capturing on the Windows loopback interface to WinPCap, a 30 day trial of [TamoSoft CommView](http://www.tamos.com/products/commview/) is probably the best bet - it saves files in a number of formats (including the LibPCap format, and a proprietary format that supports multiple link types which is also supported by Wireshark)
  * For capturing 802.11 traffic on Windows Vista or Windows 7 machines, [Microsoft Network Monitor 3.4](http://www.microsoft.com/downloads/details.aspx?familyid=983b941d-06cb-4658-b7f6-3088333d062f&displaylang=en) is worth a try - although it saves 802.11 traces with a proprietary header that's only supported by NM itself, and versions of Wireshark after 1.5.0 [r33583](https://code.google.com/p/understand/source/detail?r=33583)

## File System Implementations ##
  * An implementation of several variants of the UCSD Pascal/P-System file system is available [here](http://ucsd-psystem-fs.sourceforge.net/)