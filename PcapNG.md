## pcap-ng File Format ##
  * The [pcap-ng](http://wiki.wireshark.org/Development/PcapNg) file format was intended to supersede the previous [libpcap file format](http://wiki.wireshark.org/Development/LibpcapFileFormat) in the long-term, and fixes several shortcomings and limitations in that file format
  * As of writing, the current draft specification is [here](http://www.winpcap.org/ntar/draft/PCAP-DumpFileFormat.html), and is subject to change at any time
  * A number of sample captures, containing several different protocols, link-layer types and format features are available on our [Downloads](http://code.google.com/p/understand/downloads/list) page (tagged with "[ntar](http://code.google.com/p/understand/downloads/list?q=label:ntar)" and "[pcapng](http://code.google.com/p/understand/downloads/list?q=label:pcapng)")
  * Additional sample files are available at [this page](http://wiki.wireshark.org/Development/PcapNg) on the Wireshark Wiki
  * There is a [bug](http://tcpreplay.synfin.net/trac/ticket/23) on the [TCPreplay project](http://tcpreplay.synfin.net/) bug tracker requesting support for pcap-ng, although it seems that support has not been implemented yet

## Applications That Should Support pcap-ng, But Don't ##
  * [AirCrack-NG](http://www.aircrack-ng.org) doesn't appear to have any bugs/requests filed against it for pcap-ng support
  * Microsoft Network Monitor (any version) doesn't support pcap-ng files, and it probably won't. (Come on! You can even add proprietary extensions if you must, as long as they don't break other applications).
  * The Linux BlueZ `hcidump` utility supports its own custom file format, and a `btsnoop` file format, but not pcap-ng
  * The `pppdump` utility records packets in a custom file format, which as of late converts cleanly into a PCap-NG file (since support for the PPP direction bit in packet headers has been added to Wireshark and LibPCap)
  * [TamoSoft](http://www.tamosoft.com) [CommView](http://www.tamos.com/products/commview/) supports its own proprietary, but [documented](http://www.tamos.com/htmlhelp/commview/logformat.htm) format, in addition to libpcap and Microsoft Network Monitor formats, but not pcap-ng

## Current Issues and Bugs ##
### Wireshark/dumpcap (1.3.x/SVN trains) ###

Please note that significant enhancements have been made to pcap-ng handling in the latest SVN revisions of Wireshark, and some of these issues may only manifest themselves when working with older pcap-ng files. Depending on the issue at hand, a new capture file may be necessary to replace an existing one that cannot be parsed correctly.

  * Merging capture files containing multiple link types encapsulated in ERF frames (e.g. InfiniBand/InfiniBand Link) no longer seems to work with PCap-NG as of 1.3.6-SVN-32817. Strangely, it is however possible to convert capture files containing ERF frames to the legacy LibPCap file format, and then merge those new files into a PCap-NG file
  * Saving [DPNSS](http://en.wikipedia.org/wiki/DPNSS) packets from [EyeSDN trace files](http://understand.googlecode.com/files/D-1-Anonymous-Anonymous-D-OFF-27d01m2009y-00h00m00s-0a0None.trc) into pcap-ng files produces packets with `WTAP_ENCAP` set to `0`, and the data cannot be dissected - it seems that there is no DLT value for DPNSS at present

  * `Juniper ATM1 PIC` `VC-MUX` packets in libpcap files become `ATM OAM Cell` packets when saved into pcap-ng files, and cannot be dissected for a currently unknown reason

  * It appears that it is not currently possible to export Bluetooth HCI H1 packets from Symbian OS btsnoop capture files to pcap-ng



## Fixed Issues ##
### Wireshark/dumpcap (1.2.x/1.3.x/SVN trains) ###
  * It was possible to crash versions of Wireshark and dumpcap prior to 1.3.0 (SVN [revision 28851](https://code.google.com/p/understand/source/detail?r=28851)) whilst loading some pcap-ng files with a large number of packets, or beyond a certain (unknown) size - see [here](http://understand.googlecode.com/files/USB_DVB_New.ntar.bz2) or the bug for sample files - Reported as bug [3565](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3565), which is now resolved as of SVN [Revision 28850](https://code.google.com/p/understand/source/detail?r=28850)

  * Storing Linux mmapped USB packets in pcap-ng files produces files with unusable metadata (e.g. all packets are dissected as `URB_ISOCHRONOUS` regardless of type) - Reported as [bug 3560](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3560) - Fixed in SVN [Revision 28857](https://code.google.com/p/understand/source/detail?r=28857)

  * It appears that Apple [IP-over-1394](http://understand.googlecode.com/files/Apple1394.cap) packets within libpcap files are "lost"/"become invisible" when converted to pcap-ng files, and cannot be accessed with Wireshark, although they are still in the file - Reported as [Bug 3620](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3620)

  * Raw MTP2 packets in libpcap files are also lost when converting them to pcap-ng, example file [here](http://understand.googlecode.com/files/ansi_tcap_over_itu_sccp_over_mtp3_over_mtp2.pcap) - See [Bug 3620](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3620) - Fixed in SVN Revisions 28864-28866 to varying degrees between each revision

  * I<sup>2</sup>C/IPMB bus and event type information is lost when packets from libpcap files are saved as pcap-ng (bus number is reset to `255`, and event type is set to `0x4783c623` (`unknown state event`) - Fixed in SVN Revisions 28864-28866 to varying degrees between each revision, does not apply retroactively to existing files

  * PPPdump DCE/DTE direction information is lost, after conversion to pcap-ng - reported as [Wireshark bug 3619](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3619)

### Wireshark 1.0.7 ###
  * The bug in Wireshark 1.0.7 [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3524) mentions issues related to Interface IDs in `Interface Description Blocks` and `Enhanced Packet Blocks` - this was fixed in Wireshark 1.2.0pre2, although the information may be useful for people working with files produced by this early version of Wireshark

## Mailing Lists ##
Evolution of the pcap-ng file format is driven by several mailing lists. These are splintered between the following:
  * [wireshark-dev](http://www.mail-archive.com/wireshark-dev@wireshark.org/)
  * [ntar-workers](http://www.winpcap.org/pipermail/ntar-workers)