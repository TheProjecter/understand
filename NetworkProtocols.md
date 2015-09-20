# Banyan VINES Protocols #
  * A copy of the [VINES Protocol Definition](http://banyan.bamertal.com/Banyan-supplier-help/ProtoDef/ProtoDefMain.htm) documents (crucial for anyone interested in implementing the protocol in any manner, or understanding how it works) have been found
  * Additional resources of interest are available [here](http://banyan.bamertal.com/)

## Banyan VINES IP ##
  * EtherType is `0x0bad`
  * Currently supported by [Wireshark](http://www.wireshark.org)

## CCSDS ##
  * A sample capture file containing a number of CCSDS packets encapsulated in modified Ethernet framing are available [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3153)

# Controller Area Network #
  * A sample traffic capture file, containing various frames with SocketCAN encapsulation is available [here](http://code.google.com/p/understand/downloads/detail?name=CANtest.pcap&can=2&q=)

# DEC DNA Routing #
  * EtherType is `0x6003`
  * Currently supported by [Wireshark](http://www.wireshark.org)
# DOCSIS #
  * A sample capture file containing DOCSIS Management traffic and IP traffic encapsulated in MPEG-2 Transport Stream framing; and Wireshark configuration information for dissecting it is available [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4204)

# Frame Relay #
  * A sample traffic capture file, containing Frame Relay, Q.933, LMI, DNS, Inverse ARP, and EIGRP packets is available [here](http://code.google.com/p/understand/downloads/detail?name=Frame_Relay_Sample_1.cap&can=2&q=).

# IEEE 1394/FireWire #
  * A number of trace files containing IEEE 1394 Isochronous frames from a Mark-of-the-Unicorn 828mkII audio device are available [here](http://www.atrad.com.au/~jwoithe/motu/) (in ISODump format)
  * Additional information about that device, and some more trace files are available [here](http://www.olafchrist.de/ieee1394/)

# LANtastic #
  * EtherType is `0x81d7`
  * Currently not supported by [Wireshark](http://www.wireshark.org)
  * A sample traffic capture file is [here](http://understand.googlecode.com/files/LANtastic_Broadcasts.pcap)
  * Also makes use of the UDP-based [NetBIOS Datagram Service protocol](http://en.wikipedia.org/wiki/NetBIOS#Datagram_distribution_service)
  * Possible to install the reference implementation under Windows Vista/7 with some work

# MPLS #
  * CESoPSN and SAToP dissectors and capture files are available [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3397)

# "Raw" NetBIOS #
  * It is possible to install Microsoft's implementation (from Windows XP) under Windows Vista/7, according to [this page](http://www.mac-net.com/174984.page)

# Xerox Network Services (XNS) #
## NetBSD 3.x ##