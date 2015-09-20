# Introduction #

Add your content here.

## Firmware ##

### Embedded HTTP Server ###

  * Seems to implement only HTTP/1.0, and returns the header "`Server:HTTP/1.0\r\n`" in its responses to requests

  * Serves a number of Java class files from a virtual root directory, and from the `/wjjava/snmp/` directory, including:

  * `SNMPBinding.class`
  * `MsgBox.class`
  * `Home.class`

Judging from a brief overview of a network trace file that I created whilst configuring the server, strings included in these classes include references to "`Venice`", copyright statements, SCM usernames, ASN.1, and IPX - although I have not taken the time to manually download/extract, and decompile these.

### Telnet Interface ###
  * A basic Telnet session involving connecting to the server, retrieving help information, and then dumping the device configuration:
```
telnet 192.168.1.69
Trying 192.168.1.69...
Connected to 192.168.1.69.
Escape character is '^]'.

HP JetDirect

Please type "?" for HELP, or "/" for current settings
> ?

	To Change/Configure Parameters Enter: 
	Parameter-name: value <Carriage Return>

	Parameter-name	Type of value 
	ip:		IP-address in dotted notation 
	subnet-mask:	address in dotted notation (enter 0 for default) 
	default-gw:	address in dotted notation (enter 0 for default) 
	syslog-svr:	address in dotted notation (enter 0 for default) 
	idle-timeout:	seconds in integers 
	set-cmnty-name:	alpha-numeric string (32 chars max) 
	host-name:	alpha-numeric string (upper case only, 32 chars max) 
	dhcp-config: 	0 to disable, 1 to enable 
	allow:		<ip> [mask] (0 to clear, list to display, 10 max) 
	addrawport:	<TCP port num> (<TCP port num> 3000-9000) 
	deleterawport:	<TCP port num>  
	listrawport:	(No parameter required) 
	ipx/spx: 	0 to disable, 1 to enable 
	dlc/llc: 	0 to disable, 1 to enable 
	banner: 	0 to disable, 1 to enable 

	Type passwd to change the password.

 Type "?" for HELP, "/" for current settings or "quit" to save-and-exit.
 Or type "exit" to exit without saving configuration parameter entries 
> /

   ===JetDirect Telnet Configuration===
	Firmware Rev.	: F.08.20
	MAC Address	: 00:01:e6:5b:ff:14
	Config By	: DHCP 

	IP Address	: 192.168.1.69
	Subnet Mask	: 255.255.255.0
	Default Gateway	: 192.168.1.1
	Syslog Server	: Not Specified
	Idle Timeout	: 90 Seconds
	Set Cmnty Name	: Not Specified
	Host Name	: NPI5BFF14

	DHCP Config	: Enabled 
	Passwd		: Disabled 
   	IPX/SPX      	: Enabled 
   	DLC/LLC     	: Enabled 
	Banner page	: Enabled 
> exit

 EXITING WITHOUT SAVING ANY ENTRIES 
> Connection closed by foreign host.
```
## External Hardware ##
  * 10BaseT Ethernet port (RJ-45)
  * Centronics/Parallel printer port
  * Server Test button
  * 9-35 VDC mains adapter socket

## Compatible Mains Adapters (Non-HP) ##
  * Panasonic AC Adapter model  [FFJ9140002](http://www.amazon.co.jp/%E3%83%91%E3%83%8A%E3%82%BD%E3%83%8B%E3%83%83%E3%82%AF-Panasonic-%E3%83%8A%E3%83%8E%E3%82%A4%E3%83%BC%E7%99%BA%E7%94%9F%E6%A9%9F%E7%94%A8AC%E3%82%A2%E3%83%80%E3%83%97%E3%82%BF%E3%83%BC-%E3%83%96%E3%83%A9%E3%83%83%E3%82%AF-FFJ9140002/dp/B008H0FFK0) (Input voltage: 100V @ ~50/60Hz; Output voltage: 13.5V @ 0.8A) - supplied with Japanese Domestic Market "NanoE" humidifiers

## Internal Hardware ##

  * Access to the motherboard is provided after removing two Torx screws, located on the bottom of the device. I found that the thicker blade of a pair of large, cheap hairdressing scissors was capable of undoing them - but use of a Torx screwdriver is recommended...

### Motherboard (Front) ###
![http://lh4.googleusercontent.com/-W1WLTNuH0vM/Uq8-CfjDd-I/AAAAAAAAFgY/z3aV-iUai8g/s400/IMG00974-20131216-1643.jpg](http://lh4.googleusercontent.com/-W1WLTNuH0vM/Uq8-CfjDd-I/AAAAAAAAFgY/z3aV-iUai8g/s400/IMG00974-20131216-1643.jpg)

### Motherboard (Reverse) ###
![http://lh4.googleusercontent.com/--ZkBE3-f6AQ/Uq8-CbeXoCI/AAAAAAAAFgY/RIjius1sAYE/s400/IMG00975-20131216-1644.jpg](http://lh4.googleusercontent.com/--ZkBE3-f6AQ/Uq8-CbeXoCI/AAAAAAAAFgY/RIjius1sAYE/s400/IMG00975-20131216-1644.jpg)

### Intel 802.3/Ethernet Media Access Controller/AUI Chip ###
  * A datasheet for the [LXT908PC](http://www.digchip.com/datasheets/parts/datasheet/227/LXT908PC.php) Ethernet MAC chip is available.

### Pulse PE-68041 Isolation Transformer Chip ###

  * A datasheet for the [PE-68041](http://www.datasheetarchive.com/dlmain/Datasheets-8/DSA-151194.pdf) isolation transformer by Pulse Engineering is available.

### Motorola LM317D2T Voltage/Thermal(?) Regulator Chip ###

  * A series of [datasheets](http://www.datasheetcatalog.com/datasheets_pdf/L/M/3/1/LM317D2T.shtml) for what seem to be third-party clones of the LM317D2T chip are available. I do not know which corresponds precisely to the chip on the motherboard.

### Agilent 1QM7-0003 Chip ###
  * I have not yet been able to determine the purpose of this (SoC?) chip, although it seems that a few companies may distribute it.

### Oki/OkiData MS4V16258B-45J Chip ###
  * Have been unable to find a datasheet, or supplier information - but I suspect that this be a co-processor implementing support for a page definition language, or a memory chip, given the presence of another OkiData chip.
    * This chip was probably custom-designed for this product.

### Oki/OkiData 1818-8754 Chip ###
  * Marked with "(C) 00 HP - iIPS R27V1602E-56 1392BA1". Purpose unknown; maybe custom-designed.

## Supported Protocols ##
  * IPv4
  * Novell IPX
  * SNMP via Java-based configuration utility
  * HTTP
  * [IBM DLC/LLC](http://h30499.www3.hp.com/t5/Black-and-White/What-is-DLC-LLC/td-p/4846949#.Uq86Cjz5OtU)
  * DHCP/BootP
  * Telnet

## Official Manuals ##

  * [HP Jetdirect Print Server 170X Installation and Configuration Guide](http://h20565.www2.hp.com/portal/site/hpsc/template.BINARYPORTLET/public/kb/docDisplay/resource.process/?javax.portlet.begCacheTok=com.vignette.cachetoken&javax.portlet.endCacheTok=com.vignette.cachetoken&javax.portlet.rid_ba847bafb2a2d782fcbb0710b053ce01=docDisplayResURL&javax.portlet.rst_ba847bafb2a2d782fcbb0710b053ce01=wsrp-resourceState%3DdocId%253Demr_na-c00758101-1%257CdocLocale%253D&javax.portlet.tpst=ba847bafb2a2d782fcbb0710b053ce01_ws_BI&ac.admitted=1387215260922.876444892.492883150)

Add your content here.  Format your content with:
  * Text in **bold** or _italic_
  * Headings, paragraphs, and lists
  * Automatic links to other wiki pages