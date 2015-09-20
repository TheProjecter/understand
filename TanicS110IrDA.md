# Frame Samples #
All of these full-length frame samples are taken from the `SEMC-IrDA.cap` trace file that's available [here](http://understand.googlecode.com/files/SEMC-IrDA.cap.bz2).

## Sample 1 ##
```
No.     Time        Source                Destination           Protocol Info
  21925 497.332749  host                  5.2                   USB      URB_BULK

Frame 21925 (65 bytes on wire, 65 bytes captured)
    Arrival Time: Jul 25, 2010 23:06:44.533075000
    [Time delta from previous captured frame: 0.167289000 seconds]
    [Time delta from previous displayed frame: 0.167289000 seconds]
    [Time since reference or first frame: 497.332749000 seconds]
    Frame Number: 21925
    Frame Length: 65 bytes
    Capture Length: 65 bytes
    [Frame is marked: False]
    [Protocols in frame: usb]
    [Coloring Rule Name: IrDA Bridge/Other Device]
    [Coloring Rule String: usb.bInterfaceClass == 0x00 ]
USB URB
    URB id: 0x00000000cb0e7a00
    URB type: URB_SUBMIT ('S')
    URB transfer type: URB_BULK (3)
    Endpoint: 0x02
    Device: 5
    URB bus id: 6
    Device setup request: not present ('-')
    Data: present (0)
    URB status: Operation now in progress (-EINPROGRESS) (-115)
    URB length [bytes]: 41
    Data length [bytes]: 41
    [Response in: 21926]
    [bInterfaceClass: Use class info in Interface Descriptor (0x00)]
    Application Data: 55AA2500C0C0C0C0C0C0C0C0C0C0C0FF3F01D7210000FFFF...

0000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0010  00 00 00 00 00 00 00 00 55 aa 25 00 c0 c0 c0 c0   ........U.%.....
0020  c0 c0 c0 c0 c0 c0 c0 ff 3f 01 d7 21 00 00 ff ff   ........?..!....
0030  ff ff 01 ff 00 84 25 00 48 4f 53 54 31 00 3e 31   ......%.HOST1.>1
0040  c1                                                .
```

## Sample 2 ##
```
No.     Time        Source                Destination           Protocol Info
  21996 502.753535  5.3                   host                  USB      URB_BULK

Frame 21996 (66 bytes on wire, 66 bytes captured)
    Arrival Time: Jul 25, 2010 23:06:49.953861000
    [Time delta from previous captured frame: 0.001628000 seconds]
    [Time delta from previous displayed frame: 0.001628000 seconds]
    [Time since reference or first frame: 502.753535000 seconds]
    Frame Number: 21996
    Frame Length: 66 bytes
    Capture Length: 66 bytes
    [Frame is marked: False]
    [Protocols in frame: usb]
    [Coloring Rule Name: IrDA Bridge/Other Device]
    [Coloring Rule String: usb.bInterfaceClass == 0x00 ]
USB URB
    URB id: 0x00000000c6c58480
    URB type: URB_COMPLETE ('C')
    URB transfer type: URB_BULK (3)
    Endpoint: 0x83
    Device: 5
    URB bus id: 6
    Device setup request: not present ('-')
    Data: present (0)
    URB status: Success (0)
    URB length [bytes]: 42
    Data length [bytes]: 42
    [Request in: 21995]
    [Time from request: 0.001628000 seconds]
    [bInterfaceClass: Use class info in Interface Descriptor (0x00)]
    Application Data: FFFFFFFFFFFFFFFFFFFFC0FEBF018F710000D72100000503...

0000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................
0010  00 02 00 00 00 00 00 00 ff ff ff ff ff ff ff ff   ................
0020  ff ff c0 fe bf 01 8f 71 00 00 d7 21 00 00 05 03   .......q...!....
0030  00 91 24 00 53 6f 6e 79 20 45 72 69 63 73 73 1f   ..$.Sony Ericss.
0040  4d c1                                             M.
```

## Potential Reference Materials ##
  * The STIR4200 Linux driver source at [Kernel.org](http://www.kernel.org/home/ftp/pub/scm/linux/kernel/git/daniel/linux-tux3/drivers/net/irda/stir4200.c) describes certain aspects of frame construction, from the perspective of an otherwise unrelated device