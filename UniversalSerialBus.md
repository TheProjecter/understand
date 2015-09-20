# Devices #

  * [BT Voyager 210](BTVoyager210.md) ADSL residential gateway

  * EA-branded LogiTech microphone (trace available [here](http://code.google.com/p/understand/downloads/detail?name=LogiTech_Generic_Microphone.ntar&can=2&q=))

  * Sony Ericsson C510 mobile phone ([MTP endpoint trace](http://code.google.com/p/understand/downloads/detail?name=SEMC-C510-MTP_Linux-gnomad2.pcap.gz&can=2&q=))

  * Trust-branded PixArt 3-button/scroll-wheel optical mouse (trace available [here](http://code.google.com/p/understand/downloads/detail?name=PixArt_Trust_Optical_Mouse.ntar))

  * Nokia N73 smartphone
    * [PictBridge qualifiers trace](http://code.google.com/p/understand/downloads/detail?name=PictBridge-Nokia-Device-Qualifiers.pcap)
    * [ISI/PhoNet trace](http://code.google.com/p/understand/downloads/detail?name=Nokia_N73_ISI_Test.cap)

  * A Western Digital 500GB external hard disk drive ([a number of USB Mass Storage trace files in a BZip2'd TARball](http://understand.googlecode.com/files/Western_Digtal_USB_HDD_Transactions.tar.bz2))

  * Thomson Telecom SpeedTouch 330 ADSL modem/ATM adapter ([connection and firmware initialisation trace](http://code.google.com/p/understand/downloads/detail?name=Thomson_SpeedTouch_330_Connection_and_Firmware_load_1.cap))

  * [ZTE MF627](http://code.google.com/p/understand/wiki/ZTEMF627) UMTS/HSDPA/GPRS/EDGE modem

# Software #
## Protocol Analysis ##
### Wireshark ###
  * As of SVN [revision 33021](https://code.google.com/p/understand/source/detail?r=33021) of Wireshark, improvements have been made to both support of PPP-over-USB using [RFC 1662](http://tools.ietf.org/html/rfc1662) HDLC-like framing, and "native" PPP as part of the USB Communications Device Class - meaning that higher-layer protocols such as IPv4, and PPP CHAP are now dissected (although issues still remain around fragmented packets)
  * Support for Ethernet CDC is available using the patch attached to [Bug #4819](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4819), at a cost of breaking the dissection of other protocols encapsulated in USB\_BULK URBs
  * Support for MPEG-2 Transport Stream payloads is available using the patch attached to [Bug #4814](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4814)
  * Support for some form of ATM over USB is unimplemented
  * Support for most of the USB Mass Storage Class (and SCSI); most of the USB Hub Class; and parts of the USB Human Interface Device class has been implemented prior to that revision, for a while
  * Support for [AT commands](http://vmlemon.wordpress.com/2011/05/11/contributing-an-at-commands-dissector-to-wireshark/) on `URB_BULK` channels was added in [SVN revision 37045](http://anonsvn.wireshark.org/viewvc?view=revision&revision=37045).

# Protocols #

|<b>Protocol</b>|<b>Encapsulation</b>|<b>Device</b>|<b>Additional Information</b>|
|:--------------|:-------------------|:------------|:----------------------------|
|Ethernet       |6 byte header, additional padding after Ethernet data|Samsung CMC-730-based WiMAX device|A hex dump of an Ethernet payload in a USBSnoop log is available, [here](http://code.google.com/p/madwimax/wiki/ProtocolSummary)|
|ISI/PhoNet     |2 byte header (`0x001B`)|Nokia N73 smartphone|A Wireshark dissector for handling USB-encapsulated ISI/PhoNet frames is linked to from [this](http://vmlemon.wordpress.com/2010/12/25/wireshark-usb-phonet-dissector/) blog post|
|ISO/IEC 13818-1|USB framing only    |Pinnacle 72e USB DVB-T receiver|A sample trace file containing tuning events and MPEG-2 Transport Stream data is available,  [here](http://code.google.com/p/understand/downloads/detail?name=USB_DVB_New.ntar.bz2)|

## Asynchronous Transfer Mode (ATM) ##
### Alcatel SpeedTouch 330 Implementation ###

The Alcatel SpeedTouch 330 utilises `URB_BULK` URBs for the majority of its data transportation requirements. AAL5 frames are often concatenated together into a single URB (without padding), for efficiency.

A trace file containing a number of frames, from which the example below is a derivative of, is available [here](http://code.google.com/p/understand/downloads/detail?name=SpeedTouch-330_ILMI_IPv4_mDNS.cap).

#### ILMI Packet Example ####

The trace file corresponding to this textual dump is available, [here](http://code.google.com/p/understand/downloads/detail?name=AlcatelILMI-2.cap).

Please refer to that URL for instructions on dissection.

```
No.     Time        Source                Destination           Protocol Info
      1 0.000000                                                ILMI      iso.3.6.1.4.1.3.1.1[Packet size limited during capture]

Frame 1: 53 bytes on wire (424 bits), 53 bytes captured (424 bits)
    Arrival Time: Dec 28, 2010 15:05:44.000000000 GMT Standard Time
    Epoch Time: 1293548744.000000000 seconds
    [Time delta from previous captured frame: 0.000000000 seconds]
    [Time delta from previous displayed frame: 0.000000000 seconds]
    [Time since reference or first frame: 0.000000000 seconds]
    Frame Number: 1
    Frame Length: 53 bytes (424 bits)
    Capture Length: 53 bytes (424 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: user_dlt:data:ilmi]
DLT: 148
Data (5 bytes)
    Data: 00000100ec
    [Length: 5]
ILMI
    version: version-1 (0)
    community: ILMI
    data: trap (4)
        trap
            enterprise: 1.3.6.1.4.1.3.1.1 (iso.3.6.1.4.1.3.1.1)
            agent-addr: 0.0.0.0 (0.0.0.0)
            generic-trap: coldStart (0)
            specific-trap: 0
            time-stamp: 0
            variable-bindings: 0 items
[Packet size limited during capture: ILMI truncated]

0000  00 00 01 00 ec 30 34 02 01 00 04 04 49 4c 4d 49   .....04.....ILMI
0010  a4 29 06 08 2b 06 01 04 01 03 01 01 40 04 00 00   .)..+.......@...
0020  00 00 02 01 00 02 01 00 43 01 00 30 0e 30 0c 06   ........C..0.0..
0030  08 2b 06 01 02                                    .+...

```