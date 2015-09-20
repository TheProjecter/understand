## Mac OS X Archival Experiment ##
It seems that not all metadata is archived by every archiving tool available for Mac OS X, and tools that claim to be able to archive a piece of metadata may not do so with full fidelity.

### What Does It Involve? ###
  * Create a new directory that contains a set of files of UNIX-specific, special types:
  1. a FIFO/named pipe file
  1. a block special file
  1. a character special file
  1. at least one symbolic link
  1. at least one hard link
  1. a socket file (or a hard link to one)

  * Create a number of Mac OS X-specific objects, including:
  1. a Finder `Burn Folder`
  1. a Finder `Smart Folder`
  1. an `Alias`
  1. a file with the Finder `Locked` (`UserImmutable`) attribute
  1. a file with the `Stationary Pad` attribute
  1. a file with a Finder `Label` (one of `Red`, `Orange`, `Yellow`, `Green`, `Blue`, `Purple` or `Grey`)
  1. a file with a Mac OS X-style `Finder Comment`
  1. a file and/or directory with a custom icon
  1. a Quarantined file

### Caveats and Historical Issues ###
Note: Some of these problems have been fixed in later versions, or have been worked around in some manner.

  * Pax and GNU TAR 1.16.1 lose [BSD Flags](http://sqrl.it/?6rdc6) when archiving files, meaning that Finder Locks are also lost
  * Pax and GNU TAR 1.16.1 refuse to archive socket files, as does STAR 1.5.1
  * STAR 1.5.1, when compiled on Mac OS X seems to choke on ACLs, and seemingly ignores all extended attributes, even when compiled with the necessary options
  * The version of XAR (1.4) shipped with Mac OS X 10.5.x contains a [bug](http://code.google.com/p/xar/issues/detail?id=49) that causes ACLs to be stripped away when archived - although they're still present in the file system itself
  * In addition XAR 1.4 doesn't seem to care about Finder Creation timestamps, or Finder Comments (exposed as a `com.apple.metadata:kMDItemFinderComment` extended attribute)
  * XAR 1.5.2 seems to have problems with archiving and restoring files containing extended attributes based upon Samba NTFS Streams, thanks to an XML generation and parsing issue that has been [reported](http://code.google.com/p/xar/issues/detail?id=70) to the developers

## Mac OS (X) File Type and Creator Codes ##
### Brief History ###
  * These have been prevalent as a means of identifying files according to the application that generated them, and the type of data that they held, since the earliest versions of the Mac OS
  * In most versions of the Mac OS, up to and including Mac OS 9.x, type/creator mappings and cached icons were held within `Desktop DB` and `Desktop DF` files stored in the root directory of a HFS or HFS+ volume
  * These database files are also used by a small number of older Carbon-based applications on Mac OS X

### Implementation ###
  * In Mac OS X, these are exposed in pseudo-extended attributes that look like this:
```
com.apple.FinderInfo:
0000   57 58 42 4E 4D 53 57 44 00 00 00 00 00 00 00 00    WXBNMSWD........
0010   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................

```
  * The file type code (e.g. `WXBN`) is always stored prior to the creator code (e.g. `MSWD`) for efficiency
  * Which really looks like this, according to `hfsdebug-lite`:
```
  # Finder Info
  fdType               = 0x5758424e (WXBN)
  fdCreator            = 0x4d535744 (MSWD)
  fdFlags              = 0000000000000000
  fdLocation           = (v = 0, h = 0)
  opaque               = 0

```

## NTFS Streams and MS-DOS/Windows Flags on HFS+ (via Samba) ##
  * When a file is created using a Windows XP (and 2000?) system, no NTFS attributes are added, and Samba pretends that the `Archive` bit is set - although this is never set on the physical host file system, and attempts to clear it are silently ignored
  * When the Windows Explorer `Summary` tab is viewed for the first time, two NTFS Streams are initialised, which correspond to the following HFS+ extended attributes:`:SUMMARYINFORMATION:$DATA` and `:{4C8CC155-6C1E-11D1-8E41-00C04FB9386D}:$DATA`
  * Running `xattr -l New\ Text\ Document.txt` reveals that the attributes contain data similar to:
```
:SUMMARYINFORMATION:$DATA:
0000   FE FF 00 00 05 01 02 00 00 00 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 01 00 00 00 E0 85 9F F2    ................
0020   F9 4F 68 10 AB 91 08 00 2B 27 B3 D9 30 00 00 00    .Oh.....+'..0...
0030   28 00 00 00 02 00 00 00 01 00 00 00 18 00 00 00    (...............
0040   00 00 00 80 20 00 00 00 02 00 00 00 E4 04 00 00    .... ...........
0050   13 00 00 00 09 08 00 00                            ........

:{4C8CC155-6C1E-11D1-8E41-00C04FB9386D}:$DATA:
0000   00                                                 .

```
  * Setting the `Category` property writes an NTFS Stream and corresponding extended attribute that looks similar to:
```
:DOCUMENTSUMMARYINFORMATION:$DATA:
0000   FE FF 00 00 05 01 02 00 00 00 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 01 00 00 00 02 D5 CD D5    ................
0020   9C 2E 1B 10 93 97 08 00 2B 2C F9 AE 30 00 00 00    ........+,..0...
0030   4C 00 00 00 03 00 00 00 01 00 00 00 28 00 00 00    L...........(...
0040   00 00 00 80 30 00 00 00 02 00 00 00 38 00 00 00    ....0.......8...
0050   00 00 00 00 00 00 00 00 02 00 00 00 E4 04 00 00    ................
0060   13 00 00 00 09 08 00 00 1E 00 00 00 09 00 00 00    ................
0070   43 61 74 65 67 6F 72 79 00 00 00 00                Category....

```
  * When the `Category` property is set, and no other properties are modified, the `:SUMMARYINFORMATION:$DATA:` and `:{4C8CC155-6C1E-11D1-8E41-00C04FB9386D}:$DATA:` extended attributes are unchanged from their initial state

### Samba Metadata Options ###
  * The manpage for `smb.conf` mentions some interesting configuration options that relate to metadata:
  1. `dos filemode =` `no`/`yes`
  1. `dos filetime resolution =` `no`/`yes`
  1. `dos filetimes =` `yes`/`no`
  1. `ea support =` `no`/`yes`
  1. `store dos attributes =` `no`/`yes`
  * The default options are listed in order of potential values, sorted by the default
  * The version that ships with Mac OS X contains even more potential options that aren't mentioned in the manpage

### Cygwin File Attributes (NTEA) ###
  * When the `CYGWIN` environment variable on a Windows client machine contains `ntea`, POSIX file permissions will be stored in NTFS Streams
  * For example, setting a file's permissions to `777` results in something similar to:
```

user..UNIXATTR:
0000   FF 01 00 00                                        ....

```

## Access Control Lists (ACLs) ##
  * Technically, these are stored within an extended attribute named `com.apple.system.Security`, although most tools that are capable of dealing with extended attributes (e.g. `xattr`) and XAR) hide it from the user, and will either ignore the content of it, or treat it as a special type of metadata when handling it
  * By default, when a file or directory is created, all privileges are either granted or otherwise inherited from the parent directory; and no extended attribute or ACL flag is present in the file system or alluded to from the user's perspective
  * For an recently-created object with ACLs, the POSIX permission bits do not change; and the `Catalog File Record` properties look similar to the following, from the perspective of `hfsdebug-lite`:
```
# Catalog File Record
  type                 = file
  file ID              = 3578569
  flags                = 0000000000001110
                       . File has a thread record in the catalog.
                       . File has extended attributes.
                       . File has security data (ACLs).
  reserved1            = 0
  createDate           = Mon Dec 28 17:22:31 2009
  contentModDate       = Mon Dec 28 17:25:17 2009
  attributeModDate     = Wed Dec 30 00:34:07 2009
  accessDate           = Wed Dec 30 00:33:12 2009
  backupDate           = 0
  # BSD Info
  ownerID              = 501 (tyson)
  groupID              = 20 (staff)
  adminFlags           = 00000000
  ownerFlags           = 00000000
  fileMode             = ----------
  linkCount            = 1
  textEncoding         = 0
  attrBlocks           = 0
```

  * From the perspective of `hfsdebug-lite`, the `com.apple.system.Security` extended attribute values and mappings for a file with the default permissions, and `Full Access` granted to the Windows XP `SYSTEM` user on a Samba share look like:
```
  # Attribute Key
  keyLength            = 62
  pad                  = 0
  fileID               = 3578569
  startBlock           = 0
  attrNameLen          = 25
  attrName             = com.apple.system.Security
  # Inline Data
  recordType           = 0x10
  reserved[0]          = 0
  reserved[1]          = 0
  attrSize             = 140 bytes
  attrData             = 01 2c c1 6d 00 00 00 00 00 00 00 00 00 00 00 00 
                             ,     m                                     
                         00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
                                                                         
                         00 00 00 00 00 00 00 04 00 00 00 00 47 ec b3 f3 
                                                              G          
                         76 19 4d 40 b7 0d 37 14 17 d1 81 db 00 00 00 01 
                          v     M  @        7                            
                         00 00 0f a6 ab cd ef ab cd ef ab cd ef ab cd ef 
                                                                         
                         00 00 00 14 00 00 00 01 00 00 0a 82 ab cd ef ab 
                                                                         
                         cd ef ab cd ef ab cd ef 00 00 00 0c 00 00 00 01 
                                                                         
                         00 00 0a 82 ab cd ef ab cd ef ab cd ef ab cd ef 
                                                                         
                         00 00 00 01 00 00 00 01 00 00 3f fe 
                                                        ?    
      # File Security Information
      fsec_magic           = 0x12cc16d
      fsec_owner           = 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
      fsec_group           = 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
      # ACL Record
      acl_entrycount       = 4
      acl_flags            = 0
        # ACL Entry
        ace_applicable     = 47 ec b3 f3 76 19 4d 40 b7 d 37 14 17 d1 81 db 
          user             = tyson
          uid              = 501
          group            = *
        ace_flags          = 00000000000000000000000000000001 (0x000001)
                             . KAUTH_ACE_PERMIT
        ace_rights         = 00000000000000000000111110100110 (0x000fa6)
                             . KAUTH_VNODE_READ_DATA
                             . KAUTH_VNODE_WRITE_DATA
                             . KAUTH_VNODE_APPEND_DATA
                             . KAUTH_VNODE_READ_ATTRIBUTES
                             . KAUTH_VNODE_WRITE_ATTRIBUTES
                             . KAUTH_VNODE_READ_EXTATTRIBUTES
                             . KAUTH_VNODE_WRITE_EXTATTRIBUTES
                             . KAUTH_VNODE_READ_SECURITY
        # ACL Entry
        ace_applicable     = ab cd ef ab cd ef ab cd ef ab cd ef 0 0 0 14 
          user             = *
          group            = staff
          gid              = 20
        ace_flags          = 00000000000000000000000000000001 (0x000001)
                             . KAUTH_ACE_PERMIT
        ace_rights         = 00000000000000000000101010000010 (0x000a82)
                             . KAUTH_VNODE_READ_DATA
                             . KAUTH_VNODE_READ_ATTRIBUTES
                             . KAUTH_VNODE_READ_EXTATTRIBUTES
                             . KAUTH_VNODE_READ_SECURITY
        # ACL Entry
        ace_applicable     = ab cd ef ab cd ef ab cd ef ab cd ef 0 0 0 c 
          user             = *
          group            = everyone
          gid              = 12
        ace_flags          = 00000000000000000000000000000001 (0x000001)
                             . KAUTH_ACE_PERMIT
        ace_rights         = 00000000000000000000101010000010 (0x000a82)
                             . KAUTH_VNODE_READ_DATA
                             . KAUTH_VNODE_READ_ATTRIBUTES
                             . KAUTH_VNODE_READ_EXTATTRIBUTES
                             . KAUTH_VNODE_READ_SECURITY
        # ACL Entry
        ace_applicable     = ab cd ef ab cd ef ab cd ef ab cd ef 0 0 0 1 
          user             = daemon
          uid              = 1
          group            = daemon
          gid              = 1
        ace_flags          = 00000000000000000000000000000001 (0x000001)
                             . KAUTH_ACE_PERMIT
        ace_rights         = 00000000000000000011111111111110 (0x003ffe)
                             . KAUTH_VNODE_READ_DATA
                             . KAUTH_VNODE_WRITE_DATA
                             . KAUTH_VNODE_EXECUTE
                             . KAUTH_VNODE_DELETE
                             . KAUTH_VNODE_APPEND_DATA
                             . KAUTH_VNODE_DELETE_CHILD
                             . KAUTH_VNODE_READ_ATTRIBUTES
                             . KAUTH_VNODE_WRITE_ATTRIBUTES
                             . KAUTH_VNODE_READ_EXTATTRIBUTES
                             . KAUTH_VNODE_WRITE_EXTATTRIBUTES
                             . KAUTH_VNODE_READ_SECURITY
                             . KAUTH_VNODE_WRITE_SECURITY
                             . KAUTH_VNODE_TAKE_OWNERSHIP


```

  * The perspective of the same object, from a Windows XP machine, using the `cacls` utility looks like:
```
cacls "Y:\New Text Document.txt"
Y:\New Text Document.txt <Account Domain not found>(special access:)
                                                   READ_CONTROL
                                                   SYNCHRONIZE
                                                   FILE_GENERIC_READ
                                                   FILE_GENERIC_WRITE
                                                   FILE_READ_DATA
                                                   FILE_WRITE_DATA
                                                   FILE_APPEND_DATA
                                                   FILE_READ_EA
                                                   FILE_WRITE_EA
                                                   FILE_READ_ATTRIBUTES
                                                   FILE_WRITE_ATTRIBUTES

                         BUILTIN\Users:(special access:)
                                       READ_CONTROL
                                       SYNCHRONIZE
                                       FILE_GENERIC_READ
                                       FILE_READ_DATA
                                       FILE_READ_EA
                                       FILE_READ_ATTRIBUTES

                         Everyone:(special access:)
                                  READ_CONTROL
                                  SYNCHRONIZE
                                  FILE_GENERIC_READ
                                  FILE_READ_DATA
                                  FILE_READ_EA
                                  FILE_READ_ATTRIBUTES

                         NT AUTHORITY\SYSTEM:F
```

## Mac OS X Smart Folders ##
  * Smart Folders are XML-serialised property lists with the file name suffix `.savedSearch` that store search queries for later reuse. They are conceptually similar to Windows's "Saved Searches"/"Search Folders".
  * An example of a query for the string "`test`" on a system-wide basis:

```

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>CompatibleVersion</key>
	<integer>1</integer>
	<key>RawQuery</key>
	<string>((true) &amp;&amp; (((* = "test*"cdw || kMDItemTextContent = "test*"cdw)))) &amp;&amp; ((* = "test*"cdw || kMDItemTextContent = "test*"cdw))</string>
	<key>RawQueryDict</key>
	<dict>
		<key>FinderFilesOnly</key>
		<true/>
		<key>RawQuery</key>
		<string>((true) &amp;&amp; (((* = "test*"cdw || kMDItemTextContent = "test*"cdw)))) &amp;&amp; ((* = "test*"cdw || kMDItemTextContent = "test*"cdw))</string>
		<key>SearchScopes</key>
		<array>
			<string>kMDQueryScopeComputer</string>
		</array>
		<key>UserFilesOnly</key>
		<true/>
	</dict>
	<key>SearchCriteria</key>
	<dict>
		<key>AnyAttributeContains</key>
		<string>test</string>
		<key>CurrentFolderPath</key>
		<array>
			<string>/Users/tysonkey</string>
		</array>
		<key>FXCriteriaSlices</key>
		<array>
			<dict>
				<key>criteria</key>
				<array>
					<string>com_apple_UserSearchStringAttribute</string>
					<integer>104</integer>
				</array>
				<key>displayValues</key>
				<array>
					<string>Items matching text</string>
					<string>test</string>
				</array>
				<key>rowType</key>
				<integer>0</integer>
				<key>subrows</key>
				<array/>
			</dict>
		</array>
		<key>FXScope</key>
		<integer>1396925814</integer>
		<key>FXScopeArrayOfPaths</key>
		<array>
			<string>kMDQueryScopeComputer</string>
		</array>
	</dict>
</dict>
</plist>


```

## Mac OS X 10.5 Finder/Spotlight Comments ##
  * Exposed in a pseudo-extended attribute that looks like this:
```
com.apple.metadata:kMDItemFinderComment:
0000   62 70 6C 69 73 74 30 30 5F 10 11 53 70 6F 74 6C    bplist00_..Spotl
0010   69 67 68 74 20 43 6F 6D 6D 65 6E 74 08 00 00 00    ight Comment....
0020   00 00 00 01 01 00 00 00 00 00 00 00 01 00 00 00    ................
0030   00 00 00 00 00 00 00 00 00 00 00 00 1C             .............

```
  * It seems that no additional extended attributes are created, although some presumably exist
  * We can extract this, scrub out the ASCII textual representation and line numbers, paste that result into a hex editor, and produce a file of type `Apple binary property list`
  * Using `plutil -convert xml1` on this file, we can attempt to create an XML representation of the comment that looks like this:
```
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<string>Spotlight Comment</string>
</plist>

```

  * For certain types of "special files", such as device node and FIFO nodes on certain file systems (e.g. UDF), Finder comments are stored inside a `cmmt` atom of type `ustr` in the `.DS_Store` file at the root of the volume.

### Experiment, Part 1 ###
  * It may possible to add a Finder comment to a new file by editing the string in the XML that was produced earlier, and converting it back into a binary property list file, like this:
  * Create a plain-text `CustomComment.plist` file containing this content:
```
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<string>Hand-crafted Comment</string>
</plist>
```
  * Check the validity of the XML file using `plutil -lint CustomComment.plist`
  * Convert it into a binary `plist` using `plutil -convert binary1 CustomLabel.plist`
  * Use `touch` to create a new, empty file named `NoComment`
  * Attempt to apply the new "comment" to `NoComment` using ``xattr -w "com.apple.metadata:kMDItemFinderComment" `cat CustomComment.plist` NoComment``
  * Notice that the Finder Comment hasn't changed, since the conversion processes are seemingly lossy (need to investigate)

### Experiment, Part 2 ###
  * Using a hex editor, and the raw binary `plist` dump that was created earlier, we can attempt to modify the comment string directly
  * Unfortunately, this doesn't produce a useful result when the `plutil -lint` function is used:
```
HexedComment.plist:
XML parser error:
	Unexpected character b at line 1
Old-style plist parser error:
	Unexpected ';' or '=' after key at line 1
```
  * Still, we can attempt to inject the new `plist` into the necessary extended attribute, like so: ``xattr -w "com.apple.metadata:kMDItemFinderComment" `cat HexedComment.plist` NoComment``
  * However, it seems that we hit a limitation as far as injecting binary data with `cat` goes, so that the attribute data gets mangled at write time
  * In addition, it seems that the shell is also attempting to execute the data inside the `plist` file, and failing with: `No such file: Comment`
  * `xattr -l` reveals that said data has been mangled:  `com.apple.metadata:kMDItemFinderComment: bplist00_Fake`
  * A similar result also occurs when attempting to inject a `.ZIP` archive: `JunkData: PK`

## Mac OS X Finder Colour Labels ##
### Red ###
  * Exposed by a pseudo-extended attribute that looks like:
```
com.apple.FinderInfo:
0000   00 00 00 00 00 00 00 00 00 0C 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................

```
  * Really looks like this, according to `hfsdebug-lite`:
```
  # Finder Info
  fdType               = 0
  fdCreator            = 0
  fdFlags              = 0000000000001100
                       . Color label = red
  fdLocation           = (v = 0, h = 0)
  opaque               = 0
```

### Orange ###
  * Exposed by a pseudo-extended attribute that looks like:
```
com.apple.FinderInfo:
0000   00 00 00 00 00 00 00 00 00 0E 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................

```
  * Really looks like this, according to `hfsdebug-lite`:
```
  # Finder Info
  fdType               = 0
  fdCreator            = 0
  fdFlags              = 0000000000001110
                       . Color label = orange
  fdLocation           = (v = 0, h = 0)
  opaque               = 0
```

### Yellow ###
  * Exposed by a pseudo-extended attribute that looks like:
```
com.apple.FinderInfo:
0000   00 00 00 00 00 00 00 00 00 0A 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................

```
  * Really looks like this, according to `hfsdebug-lite`:
```
  # Finder Info
  fdType               = 0
  fdCreator            = 0
  fdFlags              = 0000000000001010
                       . Color label = yellow
  fdLocation           = (v = 0, h = 0)
  opaque               = 0
```

### Green ###
  * Exposed by a pseudo-extended attribute that looks like:
```
com.apple.FinderInfo:
0000   00 00 00 00 00 00 00 00 00 04 00 00 00 00 00 00    ................
0010   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
```
  * Really looks like this, according to `hfsdebug-lite`:
```
  # Finder Info
  fdType               = 0
  fdCreator            = 0
  fdFlags              = 0000000000000100
                       . Color label = green
  fdLocation           = (v = 0, h = 0)
  opaque               = 0
```

## Internet-Originated Files Metadata ##
### Quarantined Files ###
  * The Quarantine status is controlled by the `com.apple.quarantine` extended attribute
  * Typically, the Quarantine data consists of a set of 4 semicolon-delimited values (a set of decimal digits of an unknown purpose - typically `0000`, an 8 character opaque ID, the name of the application that created the Quarantined file, and the application's UTI (Uniform Type Identifier) prefixed with a pipe symbol)
  * For example, for two different files downloaded using Mozilla FireFox, this looks like:
```
com.apple.quarantine: 0000;4b392bb2;Firefox;|org.mozilla.firefox
com.apple.quarantine: 0000;4b38d820;Firefox;|org.mozilla.firefox
```
  * For a [JPEG file](http://images.apple.com/startpage/images/2009/09/promo-touch-20090909.jpg) downloaded by Safari, this looks like: `com.apple.quarantine: 0000;4b3a3be6;Safari;|com.apple.Safari`

### Opaque Quarantine IDs ###
NOTE: This information may not be accurate, and is currently considered to be of draft quality.

  * It is not known if the first 3 characters of the ID vary between Mac OS X installations, applications/application types, or hardware configurations
  * For most files that the author has seen, these characters have been `4b3`, although it is not guaranteed that this will always be the case
  * It may be the case that these IDs are based upon date and time (including seconds, and smaller units of time measurement), application PID, UNIX UID number, or some other data source - although it is likely that they are also derived from the content of the file itself
  * In the case of the JPEG file mentioned earlier, it seems that at least the first 5 characters (`4b3a4`) remain static when multiple copies are made by dragging the object out of the Safari window into the `Desktop` directory
  * A rough pattern emerges, in this case (only the last 3 characters change):
```
com.apple.quarantine: 0000;4b3a40d0;Safari;|com.apple.Safari
com.apple.quarantine: 0000;4b3a4107;Safari;|com.apple.Safari
```

### Safari File Origin Info ###
  * For downloaded files, Safari creates an extended attribute named `com.apple.metadata:kMDItemWhereFroms` containing a binary property list, with the source URL for reference
  * This metadata is shown to the user in the Finder's `Get Info` dialogue box, and is also collected for use by Spotlight
  * For example, for a Web Archive containing the content of [Apple's StartPage](http://www.apple.com/startpage), this looks like:
```
com.apple.metadata:kMDItemWhereFroms:
0000   62 70 6C 69 73 74 30 30 A1 01 5F 10 1F 68 74 74    bplist00.._..htt
0010   70 3A 2F 2F 77 77 77 2E 61 70 70 6C 65 2E 63 6F    p://www.apple.co
0020   6D 2F 73 74 61 72 74 70 61 67 65 2F 08 0A 00 00    m/startpage/....
0030   00 00 00 00 01 01 00 00 00 00 00 00 00 02 00 00    ................
0040   00 00 00 00 00 00 00 00 00 00 00 00 00 2C          .............,
```
  * `plutil -convert xml1` will decompose this into XML that looks like:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
	<string>http://www.apple.com/startpage/</string>
</array>
</plist>
```
  * For the JPEG that was mentioned earlier, the File Origin information looks like:
```
com.apple.metadata:kMDItemWhereFroms:
0000   62 70 6C 69 73 74 30 30 A1 01 5F 10 49 68 74 74    bplist00.._.Ihtt
0010   70 3A 2F 2F 69 6D 61 67 65 73 2E 61 70 70 6C 65    p://images.apple
0020   2E 63 6F 6D 2F 73 74 61 72 74 70 61 67 65 2F 69    .com/startpage/i
0030   6D 61 67 65 73 2F 32 30 30 39 2F 30 39 2F 70 72    mages/2009/09/pr
0040   6F 6D 6F 2D 74 6F 75 63 68 2D 32 30 30 39 30 39    omo-touch-200909
0050   30 39 2E 6A 70 67 08 0A 00 00 00 00 00 00 01 01    09.jpg..........
0060   00 00 00 00 00 00 00 02 00 00 00 00 00 00 00 00    ................
0070   00 00 00 00 00 00 00 56                            .......V
```

## A Mac OS 7.0.1 Alias ##
![http://understand.googlecode.com/files/MacOS701AliasFixed.png](http://understand.googlecode.com/files/MacOS701AliasFixed.png)
## Mac OS 7.0.1 User, Group, and Member files ##
## Mac OS X 10.6 Bookmarks ##

## Universal Disk Format ##
### Extended Attributes ###
### FIFOs, Block Nodes and Character Nodes ###
### Finder Aliases/Bookmarks ###
### Whiteout Nodes ###

  * It appears that creation of "whiteout" nodes using `mknod MacOSXWhiteout w` on UDF volumes under Mac OS X 10.6 fails with `mknod: MacOSXWhiteout: Operation not supported`.

## Web Internet Location files (Mac OS X 10.6) ##
  * These have a file name suffix of `.webloc`, a Mac OS creator code of `MACS` and a type code of `ilht`.
  * Web Internet Location files are treated in a similar manner to standard `Clipping` files when dropped onto an application window (i.e. their textual content is copied into a text entry widget).
  * Internally, they consist of two components:
    * An XML document containing a serialised property list, similar to:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>URL</key>
	<string>http://www.google.co.uk/</string>
</dict>
</plist>
```
    * A resource fork (exposed via the `com.apple.ResourceFork` pseudo-extended attribute) containing data similar to:
```
00000000  00 00 01 00 00 00 01 6C 00 00 00 6C 00 00 00 5A  |.......l...l...Z|
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000020  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000030  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000040  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000050  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000060  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000070  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000080  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000090  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000A0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000B0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000C0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000D0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000E0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
000000F0  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000100  00 00 00 30 00 00 00 01 00 00 00 00 00 00 00 00  |...0............|
00000110  00 00 00 02 54 45 58 54 00 00 01 00 00 00 00 00  |....TEXT........|
00000120  00 00 00 00 75 72 6C 20 00 00 01 00 00 00 00 00  |....url ........|
00000130  00 00 00 00 00 00 00 18 68 74 74 70 3A 2F 2F 77  |........http://w|
00000140  77 77 2E 67 6F 6F 67 6C 65 2E 63 6F 2E 75 6B 2F  |ww.google.co.uk/|
00000150  00 00 00 18 68 74 74 70 3A 2F 2F 77 77 77 2E 67  |....http://www.g|
00000160  6F 6F 67 6C 65 2E 63 6F 2E 75 6B 2F 00 00 01 00  |oogle.co.uk/....|
00000170  00 00 01 6C 00 00 00 6C 00 00 00 5A 00 00 00 00  |...l...l...Z....|
00000180  E0 00 00 00 00 1C 00 5A 00 02 64 72 61 67 00 00  |.......Z..drag..|
00000190  00 1A 54 45 58 54 00 00 00 26 75 72 6C 20 00 00  |..TEXT...&url ..|
000001A0  00 32 00 80 FF FF 00 00 00 00 84 34 00 08 01 00  |.2.........4....|
000001B0  FF FF 00 00 00 34 8C 34 00 08 01 00 FF FF 00 00  |.....4.4........|
000001C0  00 50 90 34 00 08                                |.P.4..|
000001c6

```