# Introduction #

Add your content here.

# ISO/IEC 7816 Contact Cards #

## Hardware ##

### EMV payment cards ###
### Orange Cash PayPass (Contact Interface) ###
  * The `pcsc-scan` utility reports:
```
tyson@UmBongo:~$ pcsc_scan 
PC/SC device scanner
V 1.4.17 (c) 2001-2009, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.5.5
Scanning present readers...
0: ACS ACR122U 00 00

Fri May  4 16:45:30 2012
 Reader 0: ACS ACR122U 00 00
  Card state: Card inserted, 
  ATR: 3B 6E 00 00 80 31 80 66 B0 84 12 01 6E 01 83 00 90 00

ATR: 3B 6E 00 00 80 31 80 66 B0 84 12 01 6E 01 83 00 90 00
+ TS = 3B --> Direct Convention
+ T0 = 6E, Y(1): 0110, K: 14 (historical bytes)
  TB(1) = 00 --> VPP is not electrically connected
  TC(1) = 00 --> Extra guard time: 0
+ Historical bytes: 80 31 80 66 B0 84 12 01 6E 01 83 00 90 00
  Category indicator byte: 80 (compact TLV data object)
    Tag: 3, len: 1 (card service data byte)
      Card service data byte: 80
        - Application selection: by full DF name
        - EF.DIR and EF.ATR access services: by GET RECORD(s) command
        - Card with MF
    Tag: 6, len: 6 (pre-issuing data)
      Data: B0 84 12 01 6E 01
    Tag: 8, len: 3 (status indicator)
      LCS (life card cycle): 00 (No information given)
      SW: 9000 (Normal processing.)

Possibly identified card (using /home/tyson/.smartcard_list.txt):
3B 6E 00 00 80 31 80 66 B0 84 12 01 6E 01 83 00 90 00
        Barclaycard Platinum VISA
```

The `ChAP.py` script reports (on a newly-personalised, non-activated card):

```
tyson@UmBongo:~/Downloads$ ./ChAP-0.1b/ChAP.py 
Failed to load symbol for: SCardCancelTransaction, /lib/libpcsclite.so.1: undefined symbol: SCardCancelTransaction!
insert a card within 10s
PSE found!
  6f: File Control Information (FCI) Template (30 bytes):
     84: DF Name (14 bytes): 1PAY.SYS.DDF01
     a5: Proprietary Information (12 bytes):
        88: Short File Identifier (1 bytes): 01
        5f2d: Language Preference (2 bytes): en
        9f11: Issuer Code Table Index (1 bytes): 01
  Checking for records:
  Record 01, File 01: length 41
      AID found: a0 00 00 00 04 10 10
  Found AID: MASTERCARD - a0 00 00 00 04 10 10
  6f: File Control Information (FCI) Template (56 bytes):
     84: DF Name (7 bytes): a0 00 00 00 04 10 10
     a5: Proprietary Information (45 bytes):
        50: Application Label (10 bytes): MASTERCARD
        87: Application Priority Indicator (1 bytes): skipping BER-TLV object!
  Processing Options:   77: Response Message Template Format 2 (14 bytes): 82 02 18 00 94 08 20 03 03 00 28 01 02 00
    Cardholder verification is supported
    Terminal risk management is to be performed
    SFI 04: starting record 03, ending record 03; 00 offline data authentication records
      record 03:    70: Record Template (19 bytes):
     9f08: Application Version Number (2 bytes): 00 02
     9f42: Application Currency Code (2 bytes): 0826 (United Kingdom)
     5f30: Service Code (2 bytes): 0221
     9f44: Application Currency Exponent (1 bytes): 02
  PIN tries left: 5
Log Format:  9f 27 01 9f 02 06 5f 2a 02 9a 03 9f 36 02 9f 52 06
  Found AID: PSD Entry - a0 00 00 00 04 10 10
  6f: File Control Information (FCI) Template (56 bytes):
     84: DF Name (7 bytes): a0 00 00 00 04 10 10
     a5: Proprietary Information (45 bytes):
        50: Application Label (10 bytes): MASTERCARD
        87: Application Priority Indicator (1 bytes): skipping BER-TLV object!
  Processing Options:   77: Response Message Template Format 2 (14 bytes): 82 02 18 00 94 08 20 03 03 00 28 01 02 00
    Cardholder verification is supported
    Terminal risk management is to be performed
    SFI 04: starting record 03, ending record 03; 00 offline data authentication records
      record 03:    70: Record Template (19 bytes):
     9f08: Application Version Number (2 bytes): 00 02
     9f42: Application Currency Code (2 bytes): 0826 (United Kingdom)
     5f30: Service Code (2 bytes): 0221
     9f44: Application Currency Exponent (1 bytes): 02
  PIN tries left: 5
Log Format:  9f 27 01 9f 02 06 5f 2a 02 9a 03 9f 36 02 9f 52 06
```

### GSM and UMTS SIM cards ###

### Tesco Mobile UK USIM card ###

  * The `pcsc-scan` utility reports:

```
ATR: 3B 9F 95 80 1F 43 80 31 E0 73 36 21 13 57 4A 33 0E 10 31 41 00 B0
+ TS = 3B --> Direct Convention
+ T0 = 9F, Y(1): 1001, K: 15 (historical bytes)
  TA(1) = 95 --> Fi=512, Di=16, 32 cycles/ETU
    125000 bits/s at 4 MHz, fMax for Fi = 5 MHz => 156250 bits/s
  TD(1) = 80 --> Y(i+1) = 1000, Protocol T = 0 
-----
  TD(2) = 1F --> Y(i+1) = 0001, Protocol T = 15 - Global interface bytes following 
-----
  TA(3) = 43 --> Clock stop: state L - Class accepted by the card: (3G) A 5V B 3V 
+ Historical bytes: 80 31 E0 73 36 21 13 57 4A 33 0E 10 31 41 00
  Category indicator byte: 80 (compact TLV data object)
    Tag: 3, len: 1 (card service data byte)
      Card service data byte: E0
        - Application selection: by full DF name
        - Application selection: by partial DF name
        - BER-TLV data objects available in EF.DIR
        - EF.DIR and EF.ATR access services: by GET RECORD(s) command
        - Card with MF
    Tag: 7, len: 3 (card capabilities)
      Selection methods: 36
        - DF selection by path
        - DF selection by file identifier
        - Short EF identifier supported
        - Record number supported
      Data coding byte: 21
        - Behaviour of write functions: proprietary
        - Value 'FF' for the first byte of BER-TLV tag fields: invalid
        - Data unit in quartets: 2
      Command chaining, length fields and logical channels: 13
        - Logical channel number assignment: by the card
        - Maximum number of logical channels: 4
    Tag: 5, len: 7 (card issuer's data)
      Card issuer data: 4A 33 0E 10 31 41 00
+ TCK = B0 (correct checksum)

Possibly identified card (using /home/tyson/.smartcard_list.txt):
3B 9F 95 80 1F 43 80 31 E0 73 36 21 13 57 4A 33 0E 10 31 41 00 B0
	SIM card O2 (UK, Pay-As-You-Go)
	Tesco Mobile (UK) SIM
```

  * Seems to be based upon the "Gemplus [GemXplore 3G](http://cosconor.fr/GSM/Divers/Others/Cours/SIM%20Cards/GemXplore3G%20V2.pdf) USIM" product, according to comparisons of ATR values from Ludovic's database beginning with `0x3B9F95801F`.

  * Unusual in that it returns an EMV-style `0x9F7F`/CPLC tag, similar to the following, according to [CardPeek](http://code.google.com/p/cardpeek/):

[![](https://lh3.googleusercontent.com/-R3nm7Dzgx0o/TwSA09hDbnI/AAAAAAAAEoY/9gCxIIt7E-U/s640/EMV_USIM.png)](http://code.google.com/p/understand/source/browse/trunk/smartcards/Tesco_Mobile_USIM_EMV.xml)

### Oddities ###
### TouchATag SAM (Secure Application Module) ###

  * The `pcsc-scan` utility reports:

```
ATR: 3B BE 95 00 00 41 03 00 00 00 00 00 00 00 00 00 02 90 00
+ TS = 3B --> Direct Convention
+ T0 = BE, Y(1): 1011, K: 14 (historical bytes)
  TA(1) = 95 --> Fi=512, Di=16, 32 cycles/ETU
    125000 bits/s at 4 MHz, fMax for Fi = 5 MHz => 156250 bits/s
  TB(1) = 00 --> VPP is not electrically connected
  TD(1) = 00 --> Y(i+1) = 0000, Protocol T = 0 
-----
+ Historical bytes: 41 03 00 00 00 00 00 00 00 00 00 02 90 00
  Category indicator byte: 41 (proprietary format)

Possibly identified card (using /home/tyson/.smartcard_list.txt):
3B BE 95 00 00 41 03 00 00 00 00 00 00 00 00 00 02 90 00
	touchatag SAM card
	Spanish University of Murcia smart ID card - Old version with CajaMurcia Banking card integrated (Maestro card) (M.Mar OS) - Also used by many others spanish universities
```

  * This SAM appears to have a partially documented command set (which I believe to be based upon the [ACOS3](http://wenku.baidu.com/view/9e687fe2524de518964b7db7.html) one, after reading [this](http://www.libnfc.org/community/topic/261/touchatag-mifare-problem/) forum post), but is unsupported by many common smartcard handling tools.

  * A combination of reverse-engineering the USB traffic generated by using the proprietary Windows client, and searching the Web for APDUs from log files lends some credence to that thought.

  * According to the `opensc-tool -c acos5 -f` command, the root of the SAM's file system contains the following objects:

```
3f00 type:  DF, size: 0
select[N/A] lock[N/A] delete[N/A] create[N/A] rehab[N/A] inval[N/A] list[N/A] 

  3f00ef01 type: iEF, ef structure: linvar, size: 0
  read[N/A] update[N/A] erase[N/A] write[N/A] rehab[N/A] inval[N/A] 

  3f00ef03 type: iEF, ef structure: linvar, size: 0
  read[N/A] update[N/A] erase[N/A] write[N/A] rehab[N/A] inval[N/A] 

```

### TouchATag SAM APDUs ###

|<b>Command</b>|<b>Response</b>|<b>Purpose</b>|
|:-------------|:--------------|:-------------|
|<font color='red'>80</font> <font color='purple'>14</font> <font color='green'>00</font> 00 08|49 21 8C 28 94 1D 8A F4 90 00|<font color='purple'>Get Card Info</font> - <font color='green'>8 byte Serial Number</font>|
|<font color='red'>80</font> <font color='purple'>14</font> <font color='green'>04</font> 00 06|30 30 36 38 38 32 90 00|<font color='purple'>Get Card Info</font> - <font color='green'>SAM ID?</font>|
|<font color='red'>80</font> <font color='purple'>14</font> <font color='green'>06</font> 00 08|41 43 4f 53 06 04 08 20 90 00|<font color='purple'>Get Card Info</font> - <font color='green'>Operating System Revision</font>|

## Software ##
  * The [OpenSC project](http://www.opensc-project.org/opensc) supply a number of tools for working with contact smartcards under Windows, Mac OS X, and Linux (plus other UNIX-esque operating systems).

## Tracing APDUs under Windows 7 (x86-64) ##

**Note:** Administrative privileges may be necessary for the successful completion of this activity.

  * Download the [apduview.zip](http://www.fernandes.org/apduview/apduview.zip) archive from [this page](http://www.fernandes.org/apduview/index.html)

  * Extract the archive's `winscard.dll` file to the location of the executable that utilises the PCSC APIs (e.g. `C:\Program Files (x86)\touchatag`).

  * Copy `C:\Windows\SysWOW64\WinSCard.dll` to the same directory as the executable, under the new name of `original.dll` (e.g. `C:\Program Files (x86)\touchatag\original.dll`).

  * Run the executable, and perform any necessary tasks that invoke PCSC APIs.

  * Quit the application, and then inspect the newly-created `winscard.txt` file.

## UFeliCa ##
  * This project's homepage is [here](http://shirou.prosou.nu/emacs-wiki/Felica-Card.html), and the latest version at the time of writing is [0.1.2](http://shirou.prosou.nu/src/ufelica/ufelica.tar.gz)

  * By default, the `ufelica` tool only works with Sony devices - although it is possible to modify it (by patching `ufelica.c`), in order to attempt to use it with the TouchATag reader.

  * An example of such a patch for the `ACR122U-FeliCa(4L)A REV:1.06` variant looks like:

```
--- ufelica.c~	2012-01-16 15:34:23.443258964 +0000
+++ ufelica.c	2012-01-16 15:34:23.471258944 +0000
@@ -80,8 +80,8 @@
 
   for (bus = busses; bus != NULL; bus = bus->next){
     for (dev = bus->devices; dev != NULL; dev = dev->next){
-      if((dev->descriptor.idVendor == USB_VENDOR_SONY) &&
-         (dev->descriptor.idProduct == USB_PRODUCT_SONY_PASORI) ){
+      if((dev->descriptor.idVendor == 0x072f) &&
+         (dev->descriptor.idProduct == 0x2200) ){
 
 	if (option_verbose > 1) { 
 	  printf("class=0x%02X, vendor=0x%04X, product=0x%04X\n",
```

  * Attempting to run the modified tool without root privileges results in:
```
tyson@UmBongo:~/ufelica$ ./ufelica 
could not set config 1: Operation not permitted
could not claim interface 0: Operation not permitted
error sending control message: Operation not permitted
error sending control message: Operation not permitted
00 00 00 00 00 00 00 00 00 00 
could not release intf 0: Operation not permitted
```

  * Running under `sudo`, with the PCSC daemon disabled results in:
```
tyson@UmBongo:~/ufelica$ sudo ./ufelica 
error sending control message: Broken pipe
error sending control message: Connection timed out
00 00 00 00 00 00 00 00 00 00 
```

  * Running under the same configuration, but with the verbose mode flag enabled results in:
```
tyson@UmBongo:~/ufelica$ sudo ./ufelica  -v
usb_bus found.
class=0x00, vendor=0x072F, product=0x2200
usb_device found.
002/003     072F/2200
open successed...
Query Type = 0
-- send init  : 00 00 ff 14 ec 62 29 89 11 25 f0 a0 02 a1 00 a2 89 a3 10 a4 03 a5 89 a6 10 1a 00/27
error sending control message: Broken pipe
error sending control message: Broken pipe
Pasori Initializing: ret=-32
start getting ID.
-- send get_id_edy  : 00 00 ff 05 fb 50 fe 00 00 00 b2 00/12
error sending control message: Connection timed out
control msg sent.
error sending control message: Connection timed out
error sending control message: Connection timed out
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
begin closing...
```

  * It seems that doing this will cause issues for other applications/services that attempt to use the card reader until it is disconnected; and the following can sometimes be seen in `dmesg`:

```
[  183.861824] usb 2-2: usbfs: USBDEVFS_CONTROL failed cmd ufelica rqt 64 rq 0 len 12 ret -110
```

## Other Information ##
  * A [paper](http://doc.utwente.nl/55705/1/dsse-tr-95-5.pdf) on the subject of smartcards and smartcard operating systems was published in 1995 by Pieter H. Hartel, and Eduard K. de Jong Frz at the University of Southampton's Department of Electronics and Computer Science.

  * A popular [database](http://ludovic.rousseau.free.fr/softwares/pcsc-tools/smartcard_list.txt) of smartcard ATR (Answer To Reset) values is maintained by [Ludovic Rousseau](http://ludovicrousseau.blogspot.com/).

  * A [database](http://www.ugosweb.com/emv/index.aspx) of EMV tag descriptions, derived from the EMVCo specifications is published by Ugo Chirico.

# 13.56 MHz RFID #

## Software ##

  * An Open Source implementation of an NFC stack, and various related utilities is available from the [LibNFC](http://www.libnfc.org/documentation/introduction) project.

  * The author of this page has released a number of small utilities, and enhancements to third-party ones in a [repository](https://bitbucket.org/vmlemon/smartcardtools) on BitBucket.

  * A link to a tool for examining data stored on Atmel CryptoRF tokens, and errata is available in [this forum post](http://www.libnfc.org/community/topic/235/solved-info-about-nfccryptorf/).

  * The [RFIDIOT](http://rfidiot.org/) project supply a package of tools for manipulating the contents of various types of RFID tokens, and examining Machine-Readable Travel Documents and EMV cards.

  * A driver that supposedly allows for use of LibNFC with generic PCSC-enabled applications is available from the <a href='http://ifdnfc.svn.sourceforge.net/'> <code>ifdnfc</code></a> project on SourceForge. <br /> This doesn't seem to build against the latest version of LibNFC:

```
ifd-nfc.c: In function ‘IFDHTransmitToICC’:
ifd-nfc.c:355:17: error: too few arguments to function ‘nfc_initiator_transceive_bytes’
/usr/local/include/nfc/nfc.h:80:19: note: declared here

```

## Datasheets ##

  * A [datasheet](http://idtronic-smarttags.com/pdfs/cards/STM%20SRI512.pdf) is available for the STMicroElectronics SRI512 ISO/IEC 14443-B chipset.

  * A [datasheet](http://www.acs.com.hk/drivers/eng/TDS_TOPAZ.pdf) is available from ACS for the InnoVision/Broadcom Topaz family of ISO/IEC 14443-A chipsets.

  * A [redacted datasheet](http://datasheets.maxim-ic.com/en/ds/MAX66040.pdf) is available for Maxim's [MAX66040](http://www.maxim-ic.com/datasheet/index.mvp/id/6203) ISO/IEC 14443-B chipset.

  * A [datasheet](http://mifare.net/index.php/download_file/view/5/) (MF0ICU1) is available for the [MiFare UltraLight](http://mifare.net/products/mifare-smartcard-ic-s/mifare_ultralight/) ISO/IEC 14443-A chipset.

  * A [datasheet](http://www.fmsh.com/english/products/FM11RF08_FS_ENG.pdf) is available for FuDan's FM11RF08 chipset (which is supposedly compatible with existing MiFare Classic implementations).

  * The [Users Manual](http://www.nxp.com/documents/user_manual/141520.pdf) for the NXP PN532 chipset is available.

  * A [manual](http://www.acs.com.hk/drivers/eng/API_ACR122U_v2.00.pdf) for a variant of the ACS ACR122U card reader is available.

## Hardware ##

### FeliCa tokens ###

### Sony FeliCa Lite RC-S701 ###

  * LibNFC's `nfc-list -v` command reports:

```
1 Felica (212 kbps) passive target(s) found:
        ID (NFCID2): 01  27  00  5d  1a  05  88  cd  
    Parameter (PAD): 00  f0  00  00  02  06  03  00  
   System Code (SC): 88  b4  

1 Felica (424 kbps) passive target(s) found:
        ID (NFCID2): 01  27  00  5d  1a  05  88  cd  
    Parameter (PAD): 00  f0  00  00  02  06  03  00  
   System Code (SC): 88  b4  

```

  * LibNFC's `nfc-read-forum-tag3` command reports:

```
Place your NFC Forum Tag Type 3 in the field...
NDEF Mapping version: 1.0
NFC Forum Tag Type 3 capacity: 208 bytes
NDEF data lenght: 60 bytes

```

libnfc.chip.pn53x - InListPassiveTarget
libnfc.driver.acr122 - TX: ff  00  00  00  09  d4  4a  01  01  00  ff  ff  01  00
libnfc.driver.acr122 - RX: d5  4b  01  01  14  01  01  27  00  5d  1a  05  88  cd  00  f0  00  00  02  06  03  00  88  b4  90  00

libnfc.chip.pn53x - InListPassiveTarget
libnfc.driver.acr122 - TX: ff  00  00  00  09  d4  4a  01  02  00  ff  ff  01  00
libnfc.driver.acr122 - RX: d5  4b  01  01  14  01  | <font color='red'>01  27  00  5d  1a  05  88  cd </font> | <font color='green'>00  f0  00  00  02  06  03  00 </font>| <font color='blue'>88  b4 </font> | 90  00

### ISO/IEC 14443-A tokens ###


### NXP MiFare Classic 4KB ###

  * LibNFC's `nfc-list -v` command reports:

```
1 ISO14443A passive target(s) found:
    ATQA (SENS_RES): 00  02  
* UID size: single
* bit frame anticollision supported
       UID (NFCID1): 7c  52  49  e4  
      SAK (SEL_RES): 18  
* Not compliant with ISO/IEC 14443-4
* Not compliant with ISO/IEC 18092
Fingerprinting based on ATQA & SAK values:
* Mifare Classic 4K
* SmartMX with Mifare 4K emulation

```

  * Using the [MFOC utility](http://code.google.com/p/nfc-tools/wiki/mfoc) under Linux, it is possible to derive the sector keys for a genuine MiFare Classic card, whilst dumping and decrypting its entire contents in a reasonable timeframe (several minutes) on a moderately powerful PC. <br /> It appears that this tool does not work properly under VirtualBox, due to latency induced by its USB passthrough implementation.

### NXP MiFare DESFire EV1 ###

  * LibNFC's `nfc-list -v` command reports:


```
1 ISO14443A passive target(s) found:
    ATQA (SENS_RES): 03  44  
* UID size: double
* bit frame anticollision supported
       UID (NFCID1): 04  8b  1f  f1  ad  26  80  
      SAK (SEL_RES): 20  
* Compliant with ISO/IEC 14443-4
* Not compliant with ISO/IEC 18092
                ATS: 75  77  81  02  80  
* Max Frame Size accepted by PICC: 64 bytes
* Bit Rate Capability:
  * PICC to PCD, DS=2, bitrate 212 kbits/s supported
  * PICC to PCD, DS=4, bitrate 424 kbits/s supported
  * PICC to PCD, DS=8, bitrate 847 kbits/s supported
  * PCD to PICC, DR=2, bitrate 212 kbits/s supported
  * PCD to PICC, DR=4, bitrate 424 kbits/s supported
  * PCD to PICC, DR=8, bitrate 847 kbits/s supported
* Frame Waiting Time: 77.33 ms
* Start-up Frame Guard Time: 0.6041 ms
* Node ADdress not supported
* Card IDentifier supported
* Historical bytes Tk: 80  
  * No COMPACT-TLV objects found, no status found
Fingerprinting based on ATQA & SAK values:
* Mifare DESFire / Desfire EV1

```

### DESFire EV1 Oyster ###

  * The `mifare-desfire-info` utility reports:

```
===> 0000   90 60 00 00 00                                   |.`...           |
<=== 0000   04 01 01 01 00 16 05 91 af                       |.........       |
===> 0000   90 af 00 00 00                                   |.....           |
<=== 0000   04 01 01 01 03 16 05 91 af                       |.........       |
===> 0000   90 af 00 00 00                                   |.....           |
<=== 0000   04 8b 1f f1 ad 26 80 00 00 00 00 00 42 08 91 00  |.....&......B...|
===> Version information for tag 048b1ff1ad2680:
UID:                      0x048b1ff1ad2680
Batch number:             0x0000000000
Production date:          week 42, 2008
Hardware Information:
    Vendor ID:            0x04
    Type:                 0x01
    Subtype:              0x01
    Version:              1.0
    Storage size:         0x16 (=2048 bytes)
    Protocol:             0x05
Software Information:
    Vendor ID:            0x04
    Type:                 0x01
    Subtype:              0x01
    Version:              1.3
    Storage size:         0x16 (=2048 bytes)
    Protocol:             0x05
===> 0000   90 45 00 00 00                                   |.E...           |
<=== 0000   0b 01 91 00                                      |....            |
Master Key settings (0x0b):
    0x08 configuration changeable;
    0x00 PICC Master Key not required for create / delete;
    0x02 Free directory list access without PICC Master Key;
    0x01 Allow changing the Master Key;
===> 0000   90 64 00 00 01 00 00                             |.d.....         |
<=== 0000   31 91 00                                         |1..             |
Master Key version: 49 (0x31)
===> 0000   90 6e 00 00 00                                   |.n...           |
<=== 0000   e0 04 00 91 00                                   |.....           |
Free memory: 1248 bytes
Use random UID: no
```

### NXP MiFare UltraLight ###

  * LibNFC's `nfc-list -v` command reports:

```
1 ISO14443A passive target(s) found:
    ATQA (SENS_RES): 00  44  
* UID size: double
* bit frame anticollision supported
       UID (NFCID1): 04  45  57  ba  34  23  80  
      SAK (SEL_RES): 00  
* Not compliant with ISO/IEC 14443-4
* Not compliant with ISO/IEC 18092
Fingerprinting based on ATQA & SAK values:
* Mifare Ultralight
* Mifare UltralightC

```

### Orange Cash PayPass Card ###

  * LibNFC's `nfc-list -v` command reports:

```
1 ISO14443A passive target(s) found:
    ATQA (SENS_RES): 00  04  
* UID size: single
* bit frame anticollision supported
       UID (NFCID1): 29  8b  cf  51  
      SAK (SEL_RES): 28  
* Compliant with ISO/IEC 14443-4
* Not compliant with ISO/IEC 18092
                ATS: 78  80  82  02  80  31  80  66  b0  84  12  01  6e  01  83  00  90  00  
* Max Frame Size accepted by PICC: 256 bytes
* Bit Rate Capability:
  * Same bitrate in both directions mandatory
* Frame Waiting Time: 77.33 ms
* Start-up Frame Guard Time: 1.208 ms
* Node ADdress not supported
* Card IDentifier supported
* Historical bytes Tk: 80  31  80  66  b0  84  12  01  6e  01  83  00  90  00  
  * Tk after 0x80 consist of optional consecutive COMPACT-TLV data objects;
    the last data object may carry a status indicator of one, two or three bytes.
    See ISO/IEC 7816-4 8.1.1.3 for more info
Fingerprinting based on ATQA & SAK values:
* JCOP31 v2.3.1
* SmartMX with Mifare 1K emulation

```

  * Using the following TAMA script, it is possible to access the EMV Payment System Environment, and obtain the name of the first application:

```
02; // Get firmware version
4A  01  00; // 1 target requested

// Select the payment system environment
40 01 00 A4 04 00 0E 31 50 41 59 2E 53 59 53 2E 44 44 46 30 31;

40 01 80 A8 00 00 02 83 00;

40 01 00 c0 00 00 26;

40 01 00 b2 00 0c 00;

40 01 00 b2 01 0c 00;

40 01 00 b2 01 0c 21;

```

### ISO/IEC 14443-B tokens ###

  * [Issue #168](http://code.google.com/p/libnfc/issues/detail?id=168) on the LibNFC project's issues list contains some details pertinent to the proprietary "14443-B'" technology used by some Calypso transport cards.

### Maxim MAX66040E-000AA+ ###

  * LibNFC's `nfc-list -v` command reports:

```
1 ISO14443B passive target(s) found:
               PUPI: a2  a6  02  00  
   Application Data: 30  00  2b  e0  
      Protocol Info: 77  21  71  
* Bit Rate Capability:
 * PICC to PCD, 1etu=64/fc, bitrate 212 kbits/s supported
 * PICC to PCD, 1etu=32/fc, bitrate 424 kbits/s supported
 * PICC to PCD, 1etu=16/fc, bitrate 847 kbits/s supported
 * PCD to PICC, 1etu=64/fc, bitrate 212 kbits/s supported
 * PCD to PICC, 1etu=32/fc, bitrate 424 kbits/s supported
 * PCD to PICC, 1etu=16/fc, bitrate 847 kbits/s supported
* Maximum frame sizes: 32 bytes
* Protocol types supported: ISO/IEC 14443-4
* Frame Waiting Time: 38.66 ms
* Frame options supported: NAD 

```

  * These cards are advertised as having a 64-bit UID, consisting of data in the `PUPI` field (e.g. `a2  a6  02  00` or `34  ab  02  00`), and data in the `Application Data` field (e.g. `77  21  71`).

  * The `Application Data` field supposedly contains the "upper 32 bits of the UID" (which appears to be consistent between new cards); and the (variable) PUPI corresponds to the "lower 32 bits of the UID".

  * It is possible to run the `Get System Information` (`0x2B`) command using this PN532 TAMA shell script on a TouchATag reader:

```
02; // Get firmware version
//4A  01  00; // 1 target requested
4a 01 03 00;
40 01 2B;
```

  * The TAMA commands are wrapped in an `InDataExchange` (`0x40`) packet that looks like `d4 40 01 2b`

  * The `Get System Information` command returns a result similar to `00 00 0f a2 a6 02 00 30 00 2b e0 00 00 13 07 b2`

### PN532 Pseudo-APDUs ###
  * ISO/IEC 14443-B

```
0000   d5 4b 01 01 50 34 ab 02 00 30 00 2b e0 77 21 71
0010   01 01 90 00
```

```
0000   d5 4b 01 01 50 a2 a6 02 00 30 00 2b e0 77 21 71
0010   01 01 90 00
```

  * DESFire EV1

```
0000   d5 4b 01 01 03 44 20 07 04 8b 1f f1 ad 26 80 06
0010   75 77 81 02 80 90 00
```

  * MiFare UltraLight

```
0000   d5 4b 01 01 00 44 00 07 04 2b 6e ba 34 23 80 90
0010   00
```

  * Sony FeliCa Lite RC-S701

```
0000   d5 4b 01 01 14 01 01 27 00 5d 1a 05 8a cd 00 f0
0010   00 00 02 06 03 00 88 b4 90 00
```

## Hardware Suppliers ##

  * Atmel of the USA have a [product sampling programme](http://www.atmel.com/forms/Samples.asp?category_id=172&family_id=671&source=getting_started). <br /> Although the order process appears to be successful (since I receive an e-mail in my university account), I have had limited success with using the confirmation URL provided in said e-mail, and have not seen any evidence of a product delivery, or further confirmation to date.

  * [Switch Science](http://trac.switch-science.com/wiki/FeliCa-international-order) of Japan supply Sony FeliCa (RC-S701) tags on an international basis, and fulfil orders promptly. They are also quick to provide refunds, should buyers accidentally make multiple payments for an order. As of writing, the grand total cost of shipping 2 tags to the UK was JPY2,168 (£19.19 according to PayPal).

  * The Identive Group of the USA appear to be supplying [Topaz 512-byte tags](http://www.identivenfc.com/google-nfc-tags/google-nfc-tags-type1.htm) on an international basis - although the author cannot vouch for the company's service, due to having never utilised it.

  * Maxim supply a number of RFID-related products through a [free sampling programme](https://shop.maxim-ic.com/storefront/searchsample.do?event=Sample&menuitem=Sample) - although shipments are slightly delayed due to requiring internal Business Manager authorisation; and a commercial or academic e-mail address is required for successful order approval. <br /> Samples ordered within the UK are usually despatched from a UK-based warehouse, if memory serves correctly.

## Other Information ##

  * The [YobiWiki](http://wiki.yobi.be/wiki/) has a fairly exhaustive [page](http://wiki.yobi.be/wiki/RFID) on Radio Frequency Identification-related content.