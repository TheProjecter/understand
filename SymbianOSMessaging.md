## Introduction ##

## Tools ##

  * "[Lapse of Reason](https://code.launchpad.net/~lapseofreason0)" has published an experimental Python script for parsing raw message dumps on [LaunchPad](https://code.launchpad.net/~lapseofreason0/+junk/symbian-messages), in addition to publishing some [documentation](http://bazaar.launchpad.net/~lapseofreason0/+junk/symbian-messages/view/head:/SymbianMessageFormat.txt) from his reverse-engineering efforts

  * A .NET-based application ([NBUExtractor](http://sourceforge.net/projects/nbuexplorer/)) seems to support extraction of formatted SMS data from back-ups created with the Nokia PC Suite for Windows


## S60 3rd Edition (Nokia N73) Implementation ##

H:\Private\1000484b\Mail2

## Symbian OS 8.1a/S60 2nd Edition Feature Pack 3 (Nokia N70) Implementation ##
### File System Layout ###
A typical directory structure containing Mail files looks like this:<br />
![http://understand.googlecode.com/files/Mail_Directory_Tree_Graph.png](http://understand.googlecode.com/files/Mail_Directory_Tree_Graph.png)

In the name of efficiency (and redundancy), an `Index` file in the root of `?:\System\Mail` is used to store one or more additional copies of messages, as well as metadata (e.g. type, source, and destination) and virtual folders. However, it seems that this file becomes fragmented over time, and sometimes tends to store copies of message data that was previously deleted from the file system.

Files are organised into (decimal) numbered directories, residing inside more (hexadecimal) numbered directories located in the root of `?:\System\Mail`, with either `_F` (containing attached files) or `_S` (containing mail messages) appended, depending on the type of content that is stored.

Settings files for MMS, SMS and e-mail are stored in the root of the `?:\System\Mail` directory structure, and it seems that they never occupy a directory, although an `_S` directory is sometimes created alongside them.

It appears that message files with related attachments are split into several chunks, stored in additional files scattered in a somewhat random manner, although the "parent" message file's namesake `_F` directory always accompanies it.

### Sample Messages ###
  * [A sample SMS message](http://understand.googlecode.com/files/00100004) obtained from the  `C:\System\Mail\00001001_S\4` directory, sent from the [Vodafone UK](http://www.vodafone.co.uk) [SMS Message Centre](http://help.vodafone.co.uk/system/selfservice.controller?CMD=VIEW_ARTICLE&ARTICLE_ID=2472&CONFIGURATION=1000&PARTITION_ID=1&RELATED_ARTICLE_CLICK=1&RELATED_ARTICLE_NAME=Why%20do%20I%20have%20charges%20on%20my%20bill%20for%20texts%20to%20+447785016005?) (`+447785016005`), and the number/name "`Google`". Contains the text "`Go to http://m.google.com/latitude?dc=lato on your mobile browser`". No other information has been determined yet.

  * [A sample Hesine message](http://understand.googlecode.com/files/00100022) obtained from the `E:\System\Mail\00001001_S\2` directory

  * A complete dump of a relatively clean `E:\System\Mail` directory containing the master Index file for reference, a sent MMS message (to an e-mail address) spread across several files (containing a text attachment and a SMIL stream), an opened, received Configuration Message (containing GPRS and MMS settings from [O2 UK](http://www.o2.co.uk)), and a received SMS message is available [here](http://understand.googlecode.com/files/Nokia_N70_Mail_Directory_1.tar.gz)