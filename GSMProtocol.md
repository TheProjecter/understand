## The GSM Protocol Stack ##
  * There is a Wikipedia entry, with some background and technical information [here](http://en.wikipedia.org/wiki/Global_System_for_Mobile_Communications)

## DCT3 GSM Traces ##
  * The Gammu/DCT3 trace format is based upon XML, without a specified DTD or schema, and contains raw packet data in hexadecimal format, encapsulated in an number of tags that provide metadata
  * A selection of GSM protocol trace files (as well as [the one](http://understand.googlecode.com/files/requesting_phone_number.xml) on our [Downloads](http://code.google.com/p/understand/downloads/list) page) are available [here](http://wiki.thc.org/gsm/debugtrace) from the THC Wiki.
  * Additional information on obtaining DCT3 trace files is available [here](https://svn.berlin.ccc.de/projects/airprobe/wiki/tracelog)
  * [Wireshark](http://www.wireshark.org) supports reading these files, as of at least 1.1.4-SVN-28442 (or maybe earlier) and the newly released [1.2.0pre1](http://www.wireshark.org/docs/relnotes/wireshark-1.2.0.html)
  * The Wireshark [bug](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3166) that spawned support