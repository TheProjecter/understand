This entry will be added to as information is obtained and/or discoveries are made.

## General Overview (.KOZ/Orange Music Player) ##
A .KOZ file appears to be a standard MP3 file at low level when displayed in a hex editor, or using certain MP3 playback software.
It is not entirely encrypted, as I expected, and could be transferred by Bluetooth and stored to an RS-MMC Flash Storage Card. (It was not Forward Locked).

The file that I obtained (`UtadaHikaru-ThisIsLove.koz`) contains the song "This Is Love" from the album "ULTRA BLUE" by Utada Hikaru (for those curious about it), and cost 1.50GBP to purchase (excluding the data transfer cost for downloading the Catalogue after installing the [Orange Media Player](OrangeMusicPlayer.md) to the Nokia N70 used for testing).

The Player application itself was not a chargeable download (it was obtained from a section of the Orange World portal that was marked as "Free", and GPRS data charges were not applied).

I am still trying to obtain a copy of the Player installer/application binary for examination outside of the handset.

As usual for most modern MP3 files, the `.KOZ` I viewed contained the magic number "`ID3`" (`0x494433`), and the usual set of ID3 tags (although the `TLEN` seems to be shorter than the real track length, or damaged), as well as a non-encrypted, Base64-encoded JPEG image file in either a `KPIC` or `PIC` (not sure from looking) tag.

At a glance, the rest of the file seems like a regular MP3 file.


## Deliberate Corruption/Encryption/Obfuscation ##
It seems as if the `.KOZ` file is deliberately corrupted, contains encrypted portions, or is otherwise obfuscated in places to prevent playback in anything but the proprietary [Orange Music Player](OrangeMusicPlayer.md) application for Symbian OS (unsure if the same applies to the Windows Mobile version, if it exists).

At present, I am unable to work out how the file has been altered to make this possible, although I have discovered that it is possible to load the file into the MPlayer application, and obtain audio that skips, plays faster than it does with the proprietary player, and contains glitches.

Several error messages are produced by MPlayer at a rate that makes them difficult to read easily, without using the `script` utility to record them to a file.
It appears that many of them relate to non-standard or missing data structures that are presumably worked around/accounted for by the Player application's playback engine/file parser.

I have placed a `script` log of these error messages [here](http://understand.googlecode.com/files/KOZ-Playback.txt.bz2), along with the extracted [JPEG image](http://house404.co.uk/KOZ/image-file.jpg), and the [.KOZ file itself](http://house404.co.uk/KOZ/UtadaHikaru-ThisIsLove.koz).

I have been unable to get a satisfactory amount of information about the file from the [Wireshark](http://www.wireshark.org) protocol analyser's MPEG Audio Layer 3/MPEG-2 dissector.

I have also not been able to play it in either the Linux or Symbian versions of RealPlayer or in Xine (although the first frame plays in Xine after changing the extension, before playback cuts out).

On Linux, RealPlayer gives an "Unsupported document type" error, even after changing the file name extension.

In addition, the file causes the `mp3-cmdline` utility to exist prematurely after the third frame, without an error message.

## `trackdbfx.dat` and `trackdbvr.dat` Files ##
It appears that two additional files are created or modified on the RS-MMC storage card, when a `.KOZ` file is downloaded.
These files are: `trackdbfx.dat` and `trackdbvr.dat`, and appear to identify the audio file with the Player application.

`trackdbvr.dat` has the ASCII magic number "`VR 2.1#`" (`0x565220322E3123`), and contains a `.KOZ` track file name, the associated track artist, track title, and the album name in UTF-16 format, along with other data of an unknown purpose.


I am unsure about what `trackdbfx.dat` is used for, or what the data contained within means, although it has an ASCII magic number of "`FX 2.1`".

## Misc Notes ##
I have determined that it is possible to crash [Orange Music Player](OrangeMusicPlayer.md) by playing a corrupt/damaged .KOZ file to the point where the file is damaged.
At least during testing, the player either closed gracefully, died and prevented applications other than the Telephone function from playing audio, or crashed other processes on the handset (including the Telephone process) and required a reboot of the handset.

I would expect that the player would present an error message and gracefully close the file, instead of crashing/freezing the handset or processes running on it.

The [Orange Media Player](OrangeMusicPlayer.md) version tested was "`Build Number: 1137.14241`", with a copyright notice of "`Copyright (c) 2003-2005 GrooveMobile`". There is also a URL given for perusal, offering copies of the Player software for public access: [http://orange.kozmusic.com](http://orange.kozmusic.com).

Although I do not know what they cover, the Player is unfortunately "`Protected by US patents` <a href='http://www.freepatentsonline.com/6137045.html'> <code>6,137,045</code></a> `and` <a href='http://www.freepatentsonline.com/6363153.html'> <code>6,363,153</code></a>", with a notice that others were/are pending in application, which could hinder attempts to build a player compatible with `.KOZ` files. (Such is the sorry state of things until some breakthrough happens, and software patents are rendered invalid, although I believe that they cannot be applied for in the UK yet, thankfully).

File format specifications are/were supposedly available, according to [IANA](http://www.iana.org/assignments/media-types/audio/vnd.audiokoz), although I have had no success so far finding them, and the PDF URL provided expired 5 years ago. :(

## A Quick Legal Notice ##
The information provided here was mostly derived from reverse-engineering publicly available materials (some of which were provided at-cost to the author) for interoperability purposes, with the belief that it is legal in the United Kingdom.

The Understand project disclaims any liability for the usage of it, and does not encourage illicit redistribution of otherwise decrypted audio content, unless the content is licensed for such use.