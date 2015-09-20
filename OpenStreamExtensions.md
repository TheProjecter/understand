Note: This content is now currently being maintained at [this location](http://openff.org/wiki/index.php/OpenStream_Specification). Updates may be synchronised to this wiki, and reformatted in the future.

# Introduction #
OpenStream may potentially be implemented either as an entirely new specification, or as a set of extensions and supporting amendment documents to the [ActivityStrea.ms](http://activitystrea.ms) [Atom Activity Schema specification](http://martin.atkins.me.uk/specs/activitystreams/activityschema). It aims to supplement it, by providing support for a number of features that are currently specific to proprietary and Open Source aggregation
systems and services, or missing from the base specification.

# Missing/Useful Features #

### FriendFeed-Specific Features ###

## Unifying/Supporting Proprietary Metadata? ##
### Plaxo Pulse RSS Extensions ###
  * Plaxo Pulse is a lifestreaming/content aggregation service provided by [Plaxo, Inc.](http://www.plaxo.com)
  * Examples of Pulse RSS feeds are available [here](http://www.plaxo.com/rss/events?ticket=47-1260279-8s8akmy38mtm4aq1sxyl) and [here](http://www.plaxo.com/rss/events?filter=me&ticket=47-1260279-s7e180y9nakrfjbrkmr5).
  * The `plaxoPulse="http://www.plaxo.com/"` XML namespace denotes Pulse-specific metadata and content

An example feed item (an imported Twitter post):<br />
`<item>`<br />
> `<guid isPermaLink="false">http://www.plaxo.com/events/show/202064487892</guid>`
> `<pubDate>Thu, 13 Aug 2009 00:54:10 +0100</pubDate>`<br />
> `<title>Tyson Key posted on Twitter</title>`<br />
> `<link>http://www.plaxo.com/events/show/202064487892</link>`<br />
> `<description><![CDATA[@<a href="http://twitter.com/symbian_markw" target="_blank">symbian_markw</a> It's all about the architecture. 'Nuff said...<p><a href="http://twitter.com/vmlemon/statuses/3275771117" target="_blank">more &raquo;</a></p>]]></description>`<br />
> `<author><![CDATA[Tyson Key]]></author>`<br /><br />

> `<plaxoPulse:pubDateUnix>1250121250</plaxoPulse:pubDateUnix>`<br />
> `<plaxoPulse:lastModified>2009-08-12 16:54:10</plaxoPulse:lastModified>`<br />
> `<plaxoPulse:authorProfile>http://www.plaxo.com/profile/show/201864723191?pk=b7694d3b3b9d9fa6de40cd0d462d4d1607f4069d</plaxoPulse:authorProfile>`
> `<plaxoPulse:feedIcon>Twitter.gif</plaxoPulse:feedIcon>`<br />
> `<plaxoPulse:authorPhoto></plaxoPulse:authorPhoto>`<br />
> `<plaxoPulse:numComments>0</plaxoPulse:numComments>`<br />
> `<plaxoPulse:numViews>0</plaxoPulse:numViews>`<br /><br />


> `</item>`

  * It may be interesting to support the `numViews` (object view count), `numComments` (object comment count) and `feedIcon` (feed favicon) attributes in the OpenStream specification. The `feedIcon` attribute may also be a worthy method of supporting [FriendFeed](http://www.friendfeed.com) service icon metadata.

### Jaiku RSS Extensions ###
  * Jaiku is a microblogging service provided by Google, Inc.

### Wakoopa RSS Extensions ###