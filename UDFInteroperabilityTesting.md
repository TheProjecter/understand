# Implementations #
## Linux `mkudffs` ##
  * Identifies itself as: Application ID: `*Linux mkudffs`, Implementer ID: `*Linux UDFFS`
  * Unless changed, the default Volume ID for a freshly-created volume is `LinuxUDF`

### Additional Information ###
A "`lost+found`" directory is created when a volume is initialised with `mkudffs`.
It doesn't seem to be possible to add Extended Attributes with either `setfattr` or `attr`.

### Version Information Strings ###
`Linux mkudffs 1.0.0b2...............Linux UDF 1.0.0-cvs (2002/02/09)..!.<linux_udf@hpesjro.fc.hp.com>`

### File System Creation ###
|`mkudffs -b 1024 -r 0x0102 --media-type=hd`|UDF [revision 1](https://code.google.com/p/understand/source/detail?r=1).02, 1024 bytes block size, Hard Disk|
|:------------------------------------------|:------------------------------------------------------------------------------------------------------------|
|`mkudffs -b 1024 -r 0x0102`                |UDF [revision 1](https://code.google.com/p/understand/source/detail?r=1).02, 1024 bytes block size, unknown/fallback type|
|`mkudffs -b 512 --media-type=hd`           |UDF [revision 2](https://code.google.com/p/understand/source/detail?r=2).01, 512 bytes block size, Hard Disk |
|`mkudffs -b 512 -r 0x0102`                 |UDF [revision 1](https://code.google.com/p/understand/source/detail?r=1).02, 512 bytes block size, unknown/fallback type|
|`mkudffs`                                  |UDF [revision 2](https://code.google.com/p/understand/source/detail?r=2).01, 2048 bytes block size, unknown/fallback type|

<br />

---

<br />
## Sun Solaris/OpenSolaris ##
  * Implementer ID: `*SUN SOLARIS UDF`
  * Supposedly possible to store symbolic links, socket files, block node files, character node files and FIFO files

### File System Creation ###
|`mkfs -F udfs  /dev/dsk/c5t0d0p0 -o psize=512`|Unknown UDF version, 512 bytes block size|
|:---------------------------------------------|:----------------------------------------|
|`mkfs -F udfs  /dev/dsk/c5t0d0p0 -o psize=1024`|Unknown UDF version, 1024 bytes block size|

### File System Mounting ###
|`mount -F udfs -o rw /dev/dsk/c5t0d0p0 /MountPoint`|UDFS driver, read-write mode, c5t0d0p0 (USB disk), defaults|
|:--------------------------------------------------|:----------------------------------------------------------|

### Mounting on Linux ###
Mount disks/images created with the Solaris implementation using "`mount -t udf -o nostrict,bs=512`", since the Linux implementation has become dumb/broken as of late.

If a NetBSD UDF file system existed on the volume, before formatting a disk under Solaris, you'll probably see in `dmesg`:<br />
`udf: Block 257 of volume descriptor sequence is corrupted or we could not read it. UDF-fs INFO UDF: Mounting volume '26eacaf8', timestamp 2009/05/09 10:53 (103c)`

It appears that it (the NetBSD volume) mounts anyway, if that's the case. Solaris stuff is probably trampled/ignored.
<br />

---

<br />

## NetBSD ##
Identifies itself as: `*NetBSD userland UDF`, `*NetBSD newfs`

### File System Creation ###
|`newfs_udf`|UDF [revision 2](https://code.google.com/p/understand/source/detail?r=2).01, supposedly 512 bytes block size/block size of disk, unknown type/"`04<REWRITABLE>`", 20% metadata, logical volume "`anonymous`"|
|:----------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`newfs_udf -v 0x102 -M`|UDF [revision 1](https://code.google.com/p/understand/source/detail?r=1).02 (min), unknown block size, unknown type, no metadata partition                                                                  |
|`newfs_udf -v 0x102 -M -s 1024`|Supposedly generates UDF [revision 1](https://code.google.com/p/understand/source/detail?r=1).02(min)-1.05(max), type 04, no metadata partition                                                             |

### Mounting/Virtual Devices ###
|`vnconfig -c vnd0 PathToDiskImage 1024/1/1/1`|Attach `vnd0` to PathToDiskImage, using 1024 bytes block size|
|:--------------------------------------------|:------------------------------------------------------------|
|`mount_udf /dev/vnd0d /mnt`                  |Supposedly mounts vnd0d on /mnt, really bails out with the error "`mount_udf: Cannot mount /dev/vnd0d on /mnt: Operation not supported by device`".|

## Mounting on Linux ##
Results in "`UDF-fs: No partition found (1)`" on Linux kernel 2.6.28-0.131.rc8.git4.fc11.i686, when no options are specified.
|`mount -t udf -o nostrict,bs=512 /dev/sdc /mnt/`|Will try and mount the NetBSD UDF volume with 512 bytes block size, no strict compliance mode.|A successful mount with this yields "`UDF-fs INFO UDF: Mounting volume '088cc6dc', timestamp 2009/05/09 14:25 (103c)`" in `dmesg`.|
|:-----------------------------------------------|:---------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------|

<br />

---

<br />

## Windows 7 ##
  * When mounted under OpenSolaris (`snv_111b`) automatically, GNOME produces an `Unable to mount the volume 'UDF Volume'` error
  * Might be possible to mount manually somehow, `/dev/dsk/c10t0d0p0`

## Apple Mac OS X 10.5.6 ##
### Metadata ###
  * Despite being POSIX-compliant, it is not possible to create FIFO nodes, character device nodes or block device nodes on a UDF volume
  * In addition, if files of the aforementioned types exist on a volume, they are simply ignored, and it is not possible to read them
  * It is possible to store Finder Info (Stationary Pad bit, and Finder Labels) inside a `*UDF Mac FinderInfo` stream

### Disc Recording Framework Variant ###
Identifies itself as: `*Apple Mac OS X DiscRec`
|`*UDF Mac VolumeInfo`|
|:--------------------|
|`*UDF Mac ResourceFork`|

# Misc Data Structures #

## DVD Video Discs/General ##
|`*UDF Toshiba DVD Video`|
|:-----------------------|
|`*UDF FreeEASpace`      |
|`*UDF DVD CGMS Info`    |
|`*UDF LV Info`          |Logical Volume Descriptor|
|`OSTA Compressed Unicode`|
|`*OSTA UDF Compliant`   |
|`*Philips DVD Video`    |

<br />

---

<br />

# Example Volumes #
  * A couple of "Live" examples of volumes created or utilised/shared by the implementations listed above are available [here](http://understand.googlecode.com/files/UDF_Sample_Volumes_1.tar.bz2)
  * A version of the "Live" examples is available with additional Mac OS X 10.5.6-specific metadata [here](http://understand.googlecode.com/files/UDF_Sample_Volumes_2.zip)
  * A (partial) example of a UDF volume created by a Philips standalone DVD+RW recorder is available [here](http://understand.googlecode.com/files/Philips_DVD%2BRW_UDF_Initial_Structure_Dump_1.img.bz2)
  * A (partial) example of a UDF volume created using the Mac OS X 10.5.6 Disc Recording framework on a DVD+RW disc is available [here](http://understand.googlecode.com/files/Mac_OS_X_10.5.6_DVD_test_1.img.bz2)
  * An empty UDF 2.01 disk image (created on Mac OS X 10.5.6) is available [here](http://understand.googlecode.com/files/UDFMacOSX.img.zip)