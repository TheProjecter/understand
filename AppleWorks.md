## Clipboard Data (Windows) ##

A drawing pasted into PuppetMaster (Qt-based application) is identified as:
```
("application/x-qt-image", "application/x-qt-windows-mime;value="Mac-PICT"") 
Selected "application/x-qt-windows-mime;value="Mac-PICT"" 
```

## MathType 2.2 (Equation Editor, Windows) Clipboard data ##
```
("application/x-qt-windows-mime;value="MathType EF"", "application/x-qt-windows-mime;value="Embed Source"", "application/x-qt-windows-mime;value="Object Descriptor"") 
```

  * Looks like padded text, if pasted into PuppetMaster
  * Hex dump with Math formatting: `02010102020a011283480000` (contains ASCII "H", and formatting)

  * Hex dump with Text formatting: `02010102020a010281480000` (contains ASCII "H", and formatting)

  * Hex dump with Formula formatting: `02010102020a010282480000` (contains ASCII "H", and formatting)

### Default styles ###
| **Style** | **Font** | **Character Format (Bold/Italic)** |
|:----------|:---------|:-----------------------------------|
| Text      | Times New Roman | No/No                              |
| Function  | Times New Roman | No/No                              |
| Variable  | Times New Roman | Italic only                        |
| L.C. Greek | Symbol   | Italic only                        |
| U.C. Greek | Symbol   | No/No                              |
| Symbol    | Symbol   | No/No                              |
| Matrix-Vector | Times New Roman | Bold only                          |
| Number    | Times New Roman | No/No                              |

### Embedded using OLE in WP document ###
  * Becomes :

```
("application/x-qt-windows-mime;value="Embedded Object"", "application/x-qt-windows-mime;value="Object Descriptor"")
```

OLE document blob containing font info, `ClarisWorks Equation 2.0MathType EFEquation.CWEE2`, and presumably raw data like the "padded text"

## WireLust ##

  * A [blog post](http://www.wirelust.com/2013/01/17/parsing-appleworks-and-clarisworks-file-formats/) about these formats was published in 2013
  * A number of example files were also [published](http://wirelust.com/examples/archiving/appleworks/)
  * 

### MacWrite, and Additional Documentation ###
  * A [CVS repository](http://libcwk.cvs.sourceforge.net/viewvc/libcwk/libcwk/), hosted on SourceForge.net contains some C source files from an attempt at writing a parser, plus some documentation on [MacWrite's formats](http://libcwk.cvs.sourceforge.net/viewvc/libcwk/libcwk/doc/)

## Related ##

  * Wikipedia's [article](http://en.wikipedia.org/wiki/PICT) on the Macintosh PICT graphics format, used in AppleWorks drawing clipboard data


## File Type and Creator Metadata ##
Common Mac OS X UTI: `com.apple.appleworks.document`<br />
Common Windows/DOS-style file name suffix: `.cwk`<br />
Most Likely Common Magic Number: `0x0607D000424F424F0607D0000000000000000000`<br />

## Classic Mac OS Type/Creator FourCC Codes ##
|<b>Creator</b>|<b>Type</b>|<b>Description</b>|
|:-------------|:----------|:-----------------|
|`BOBO`        |`CWWP`     |AppleWorks/ClarisWorks Word Processing Document|
|`BOBO`        |`CWSS`     |AppleWorks/ClarisWorks Spreadsheet Document|
|`BOBO`        |`CWDB`     |AppleWorks/ClarisWorks Database Document|
|`BOBO`        |`CWGR`     |AppleWorks/ClarisWorks Drawing Document|
|`BOBO`        |`CWPT`     |AppleWorks/ClarisWorks Painting Document|
|`BOBO`        |`CWPR`     |AppleWorks/ClarisWorks Presentation Document|