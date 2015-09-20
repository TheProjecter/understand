## Introduction ##

Orange Music Player is currently available for download [here](http://orange.kozmusic.com/), and versions for several platforms exist (Symbian OS (ARM - S60v2, [S60v3](http://orange.kozmusic.com/installs/n_n80/1208/MusicPlayer.SISX) and UIQ), Windows Mobile (ARM), and a Java version (<a href='http://orange.kozmusic.com/installs/j2me/65582/JukeBox.jar'><code>.JAR</code></a>/<a href='http://orange.kozmusic.com/installs/j2me/65582/JukeBox.jad'><code>.JAD</code></a>) intended primarily for Motorola phones.

In theory, the S60v3 version may work on S60v5/[Symbian^2](http://blog.symbian.org/2009/04/30/reviewing-the-release-plan/)-based devices, as they are also based upon Symbian OS 9.x versions, and share substantial amounts of source code and infrastructure.

## Symbian OS/S60v2 version ##

It is possible to install this version on either a handset's internal Flash memory, or on an external Flash memory card (e.g. RS-MMC or MicroSD), a number of directories and files are installed or otherwise created, and a number of files are also downloaded from an undetermined HTTP server.

## Symbian OS/S60v3 version ##
### Background/Theory ###
Now that the [Symbian Foundation](http://www.symbian.org) have released the EKA2 source code, along with a QEMU-based ARM native code emulator and baseport (Syborg), we can theoretically run the Player outside of a mobile phone for the first time. In addition, support for audio playback was recently implemented.

The availability of the new source code means that it is possible to disable/reduce the functionality of the Platform Security model and Trusted Computing Base, in order to grant all Capabilities to all processes at runtime, although this is of little use at present. We can also theoretically modify ETel to return a spoofed IMEI or telephone number to the application.

However, ETel source code has not been published yet, the Software Installation package has not been published yet (although tools are available to decompose `.SIS` files to their constituent files), a UI layer is not available at present (although TextShell/`EShell` is), and the MultiMedia Framework is also absent. In the interim, it is still possible to determine which DLLs are necessary.

## Java/J2ME version ##