# Introduction #

LANtastic used EtherType 0x81D7, and UDP port 138 (for NetBIOS Datagram Service).

# Packet Structure #

## Packet Header ##

```
0000   4e 52 00 0c 29 f0 88 c8 ff ff ff ff ff ff 00 00  NR..)...........
0010   00 00 00 00 80 00 a6 00 0e 00 00 00 00 00 00 00  ................
0020   00 00 00 00 00 01 02 5f 5f 4d 53 42 52 4f 57 53  .......__MSBROWS
0030   45 5f 5f 02 01 57 49 4e 2d 54 30 46 54 55 39 53  E__..WIN-T0FTU9S
0040   54 54 4e 35 00                                   TTN5.
```

```
0000   4e 52 00 0c 29 f0 88 c8 ff ff ff ff ff ff 00 00  NR..)...........
0010   00 00 00 00 80 00 7c 00 0e 00 00 00 00 00 00 00  ......|.........
0020   00 00 00 00 00 57 4f 52 4b 47 52 4f 55 50 20 20  .....WORKGROUP  
0030   20 20 20 20 1b 57 49 4e 2d 54 30 46 54 55 39 53      .WIN-T0FTU9S
0040   54 54 4e 35 00                                   TTN5.
```

Fields:
  * Magic Number(?) (4e 52)
  * Destination MAC Address (ff ff ff ff ff ff)
  * Source MAC Address (00 0c 29 f0 88 c8)
  * Padding?

## Proprietary Discovery? ##
```
0000   4e 52 00 0c 29 f0 88 c8 ff ff ff ff ff ff 00 00  NR..)...........
0010   00 00 00 00 80 00 21 00 0e 00 00 00 00 00 00 00  ......!.........
0020   00 00 00 00 00 4c 41 4e 74 61 73 74 69 63 2d 47  .....LANtastic-G
0030   72 6f 75 70 04 4c 54 2d 57 49 4e 2d 54 30 46 54  roup.LT-WIN-T0FT
0040   55 39 53 54 00 00                                U9ST..
```

## Server Message Block/IBM LAN Manager Tunnelling ##
```
0000   4e 52 00 0c 29 f0 88 c8 ff ff ff ff ff ff 00 00  NR..)...........
0010   00 00 00 00 80 00 8c 00 0e 00 00 00 00 00 00 00  ................
0020   00 00 00 00 00 57 49 4e 2d 54 30 46 54 55 39 53  .....WIN-T0FTU9S
0030   54 54 4e 35 00 57 49 4e 2d 54 30 46 54 55 39 53  TTN5.WIN-T0FTU9S
0040   54 54 4e 35 00 ff 53 4d 42 25 00 00 00 00 00 00  TTN5..SMB%......
0050   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
0060   00 00 00 00 00 11 00 00 16 00 00 00 00 00 00 00  ................
0070   00 00 e8 03 00 00 00 00 00 00 00 00 16 00 56 00  ..............V.
0080   03 00 01 00 01 00 02 00 27 00 5c 4d 41 49 4c 53  ........'.\MAILS
0090   4c 4f 54 5c 42 52 4f 57 53 45 00 0a 01 01 00 00  LOT\BROWSE......
00a0   00 57 49 4e 2d 54 30 46 54 55 39 53 54 54 4e 35  .WIN-T0FTU9STTN5
```

In this case (a broadcast packet that seems to correspond to an SMB `Get Backup List Response`), it seems that LANtastic encapsulates SMB packets with a ~69 byte header, containing a group name, or a machine name; and some additional, unknown data.

For some reason, Wireshark dissects this packet as "truncated", after importing the above hex payload into a trace file with a user-specified DLT value. I assume that this is related to the group/machine name data at the end of the packet.

Strings **may** be preceded by their length?

Payload length seems to be encoded in a weird way (e.g. decimal 134/0x86 -> 0x80 0x00 0xA6, or decimal 91/0x5B -> 0x52 0x4B) - Need to confirm

### Decapsulated payload example ###
```
No.     Time           Source                Destination           Protocol Length Info
      1 0.000000000                                                BROWSER  176    Get Backup List Response[Packet size limited during capture]

Frame 1: 176 bytes on wire (1408 bits), 176 bytes captured (1408 bits) on interface 0
    Interface id: 0 (Fake IF File->Import)
    Packet flags: 0x00000000
        .... .... .... .... .... .... .... ..00 = Direction: Not available (0x00000000)
        .... .... .... .... .... .... ...0 00.. = Reception type: Not specified (0)
        .... .... .... .... .... ...0 000. .... = FCS length: 0
        .... .... .... .... 0000 000. .... .... = Reserved: 0
        .... ...0 .... .... .... .... .... .... = CRC error: Not set
        .... ..0. .... .... .... .... .... .... = Packet too long error: Not set
        .... .0.. .... .... .... .... .... .... = Packet too short error: Not set
        .... 0... .... .... .... .... .... .... = Wrong interframe gap error: Not set
        ...0 .... .... .... .... .... .... .... = Unaligned frame error: Not set
        ..0. .... .... .... .... .... .... .... = Start frame delimiter error: Not set
        .0.. .... .... .... .... .... .... .... = Preamble error: Not set
        0... .... .... .... .... .... .... .... = Symbol error: Not set
    Encapsulation type: USER 7 (52)
    Arrival Time: Feb 14, 2014 23:57:48.000000000 GMT Standard Time
    [Time shift for this packet: 0.000000000 seconds]
    Epoch Time: 1392422268.000000000 seconds
    [Time delta from previous captured frame: 0.000000000 seconds]
    [Time delta from previous displayed frame: 0.000000000 seconds]
    [Time since reference or first frame: 0.000000000 seconds]
    Frame Number: 1
    Frame Length: 176 bytes (1408 bits)
    Capture Length: 176 bytes (1408 bits)
    [Frame is marked: False]
    [Frame is ignored: False]
    [Protocols in frame: user_dlt:data:smb:browser]
    [Coloring Rule Name: SMB]
    [Coloring Rule String: smb || nbss || nbns || nbipx || ipxsap || netbios]
DLT: 154
Data (69 bytes)

0000  4e 52 00 0c 29 f0 88 c8 ff ff ff ff ff ff 00 00   NR..)...........
0010  00 00 00 00 80 00 8c 00 0e 00 00 00 00 00 00 00   ................
0020  00 00 00 00 00 57 49 4e 2d 54 30 46 54 55 39 53   .....WIN-T0FTU9S
0030  54 54 4e 35 00 57 49 4e 2d 54 30 46 54 55 39 53   TTN5.WIN-T0FTU9S
0040  54 54 4e 35 00                                    TTN5.
    Data: 4e52000c29f088c8ffffffffffff00000000000080008c00...
    [Length: 69]
SMB (Server Message Block Protocol)
    SMB Header
        Server Component: SMB
        SMB Command: Trans (0x25)
        Error Class: Success (0x00)
        Reserved: 00
        Error Code: No Error
        Flags: 0x00
            0... .... = Request/Response: Message is a request to the server
            .0.. .... = Notify: Notify client only on open
            ..0. .... = Oplocks: OpLock not requested/granted
            ...0 .... = Canonicalized Pathnames: Pathnames are not canonicalized
            .... 0... = Case Sensitivity: Path names are case sensitive
            .... ..0. = Receive Buffer Posted: Receive buffer has not been posted
            .... ...0 = Lock and Read: Lock&Read, Write&Unlock are not supported
        Flags2: 0x0000
            0... .... .... .... = Unicode Strings: Strings are ASCII
            .0.. .... .... .... = Error Code Type: Error codes are DOS error codes
            ..0. .... .... .... = Execute-only Reads: Don't permit reads if execute-only
            ...0 .... .... .... = Dfs: Don't resolve pathnames with Dfs
            .... 0... .... .... = Extended Security Negotiation: Extended security negotiation is not supported
            .... .0.. .... .... = Reparse Path: The request does not use a @GMT reparse path
            .... .... .0.. .... = Long Names Used: Path names in request are not long file names
            .... .... ...0 .... = Security Signatures Required: Security signatures are not required
            .... .... .... 0... = Compressed: Compression is not requested
            .... .... .... .0.. = Security Signatures: Security signatures are not supported
            .... .... .... ..0. = Extended Attributes: Extended attributes are not supported
            .... .... .... ...0 = Long Names Allowed: Long file names are not allowed in the response
        Process ID High: 0
        Signature: 0000000000000000
        Reserved: 0000
        Tree ID: 0
        Process ID: 0
        User ID: 0
        Multiplex ID: 0
    Trans Request (0x25)
        Word Count (WCT): 17
        Total Parameter Count: 0
        Total Data Count: 22
        Max Parameter Count: 0
        Max Data Count: 0
        Max Setup Count: 0
        Reserved: 00
        Flags: 0x0000
            .... .... .... ..0. = One Way Transaction: Two way transaction
            .... .... .... ...0 = Disconnect TID: Do NOT disconnect TID
        Timeout: 1 second
        Reserved: 0000
        Parameter Count: 0
        Parameter Offset: 0
        Data Count: 22
        Data Offset: 86
        Setup Count: 3
        Reserved: 00
        Byte Count (BCC): 39
        Transaction Name: \MAILSLOT\BROWSE
SMB MailSlot Protocol
    Opcode: Write Mail Slot (1)
    Priority: 1
    Class: Unreliable & Broadcast (2)
    Size: 39
    Mailslot Name: \MAILSLOT\BROWSE
Microsoft Windows Browser Protocol
    Command: Get Backup List Response (0x0a)
    Backup List Requested Count: 1
    Backup Request Token: 1
[Packet size limited during capture: BROWSER truncated]

```