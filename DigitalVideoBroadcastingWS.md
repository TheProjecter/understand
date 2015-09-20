# Patches #
  * The patch attached to [Bug #4814](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4814) will enable support for dissection of MPEG-2 Transport Streams encapsulated in USB framing that are either being captured from a live USB capture session (only supported under Linux), or stored in a trace file on-disk. It was committed in [SVN revision 37039](http://anonsvn.wireshark.org/viewvc?view=revision&revision=37039).
  * A patch attached to [Bug #4178](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4178) claims to support dissection of DVB IP datacasts, under certain conditions
  * The patches attached to [Bug #5654](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=5654) adds support for the DVB Common Interface protocol. It was committed in [SVN revision 36163](http://anonsvn.wireshark.org/viewvc?view=revision&revision=36163).

# Somewhat Related Stuff #
  * Support for dissection of DOCSIS frames encapsulated within MPEG-2 Transport Streams has been implemented for a while, so it seems - a sample of these might be attached to [Bug #3218](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=3218)
  * [Bug #4338](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=4338) has a patch related to MPEG-2 Transport Stream PCR clock measurement/analysis
  * Avalpa have some sample files created using their Open Source OpenCaster software available [here](http://www.avalpa.com/the-key-values/15-free-software/59-opencaster-demo-roll)
  * A sample trace file containing DVB-related SimulCrypt traffic is available here [here](https://bugs.wireshark.org/bugzilla/show_bug.cgi?id=2935)
  * An MPEG-2 Transport Stream file containing data from a Japanese ISDB-T broadcast is available [here](http://mailman.videolan.org/pipermail/vlc/2008-January/015303.html)