<!--Discussion and collaboration on the tentative OpenStream specification-->

# Introduction #
OpenStream may potentially be implemented either as an entirely new specification, or as a set of extensions and supporting amendment documents to the [ActivityStrea.ms](http://activitystrea.ms) [Atom Activity Schema specification](http://martin.atkins.me.uk/specs/activitystreams/activityschema) (AAS).

It aims to supplement AAS, by providing support for a number of features that are currently specific to proprietary and Open Source aggregation systems and services, or missing from the base specification.

# Missing/Useful Features #

### FriendFeed-Specific Features ###
**Mapping of Likes to either [Save](http://martin.atkins.me.uk/specs/activitystreams/activityschema#save), [Share](http://martin.atkins.me.uk/specs/activitystreams/activityschema#share), [Mark as Favorite](http://martin.atkins.me.uk/specs/activitystreams/activityschema#favorite) or [Tag](http://martin.atkins.me.uk/specs/activitystreams/activityschema#anchor5) elements in Activity Schema Specification** Mapping of Groups/Rooms to [Group](http://martin.atkins.me.uk/specs/activitystreams/activityschema#group) elements, and extension to support privacy functionality (Private - "Only the people you invite can view and post to the feed"/Standard - "You post messages, anyone can comment"/Public - "Anyone can post messages to and comment on the feed")
**Mapping of Group/Room avatars to the "avatar" property** Extension to support Hidden items
**Imaginary Friends functionality is unsupported - an extension is necessary** Private/semi-private feeds are unsupported - an extension is necessary
**Support for FriendFeed short/long GUIDs for mapping content, room, file and user objects or OpenFF equivalents** Support for GeoRSS (```
<nowiki>xmlns:georss="http://www.georss.org/georss"

Unknown end tag for &lt;/nowiki&gt;

``` and ```
<nowiki>xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#"

Unknown end tag for &lt;/nowiki&gt;

```) should be maintained, as FriendFeed currently provides this in their hybrid Atom/RSS feeds, although it is seemingly unused at present
**It may be interesting to map some GeoRSS attributes to the [Location](http://martin.atkins.me.uk/specs/activitystreams/activityschema#anchor17)/[Place](http://martin.atkins.me.uk/specs/activitystreams/activityschema#anchor15) etc. attributes in AAS, or maintain a hybrid approach** Support for MediaRSS (```
<nowiki>xmlns:media="http://search.yahoo.com/mrss/"

Unknown end tag for &lt;/nowiki&gt;

```) should be maintained, although portions could be mapped to AAS elements and attributes
**Support for Direct Messages/multi-destination posts (generated on-the-fly, based upon privacy settings?)**

## Unifying/Supporting Proprietary Metadata? ##

### FriendFeed APIv2 XML ###
**Example XML feeds in the FriendFeed XML (FFML?) format are available [here](http://friendfeed-api.com/v2/feed/bret?format=xml), and [here](http://paster.dazjorz.com/?p=4658)** Supported features include ```
<nowiki><like>

Unknown end tag for &lt;/nowiki&gt;

```, ```
<nowiki><via>

Unknown end tag for &lt;/nowiki&gt;

```, ```
<nowiki><entry>

Unknown end tag for &lt;/nowiki&gt;

```, and ```
<nowiki><comment>

Unknown end tag for &lt;/nowiki&gt;

``` tags
**FriendFeed utilises a number of Object ID formats, most of which don't appear to have been given publicised names. These take a number of forms, including long-form GUIDs for most legacy content (e.g. (**```
<nowiki>/e/71f0c4d2-2918-44cc-a2df-6f486e96e37c

Unknown end tag for &lt;/nowiki&gt;

```), new-style "Short Hashes" (e.g. ```
<nowiki>ae4937ac

Unknown end tag for &lt;/nowiki&gt;

```, and "Long"/"Opaque" Hashes/IDs in a style similar to ```
<nowiki>e/ae4937ac7756d6c5970b0edd67cfd5b5

Unknown end tag for &lt;/nowiki&gt;

```
**As currently implemented in FriendFeed, Opaque Object (Entry) IDs are also valid URIs, that redirect to a URL containing a Short Hash, and a hyphenated extract of an Entry's title (e.g.**```
<nowiki>http://friendfeed.com/bret/ae4937ac/bret-we-need-handyman-live-in-los-gatos-anyone

Unknown end tag for &lt;/nowiki&gt;

```)
**The**```
<nowiki><like>

Unknown end tag for &lt;/nowiki&gt;

``` tag may potentially align with one of the features mentioned earlier, although extensions may be necessary to support FriendFeed-specific (meta-)metadata
**Directed/Multi-Destination Posts are handled with**```
<nowiki><to>

Unknown end tag for &lt;/nowiki&gt;

``` elements, which contain additional elements and metadata that should be considered

### Plaxo Pulse RSS Extensions ###
**Plaxo Pulse is a lifestreaming/content aggregation service provided by [Plaxo, Inc.](http://www.plaxo.com)** Examples of Pulse RSS feeds are available [here](http://www.plaxo.com/rss/events?ticket=47-1260279-8s8akmy38mtm4aq1sxyl) and [here](http://www.plaxo.com/rss/events?filter=me&ticket=47-1260279-s7e180y9nakrfjbrkmr5).
**The**```
<nowiki>plaxoPulse="http://www.plaxo.com/"

Unknown end tag for &lt;/nowiki&gt;

``` XML namespace denotes Pulse-specific metadata and content

An example feed item (an imported Twitter post):<br />

```
<nowiki><item>

Unknown end tag for &lt;/nowiki&gt;

```
:
:    ```
<nowiki><guid isPermaLink="false">http://www.plaxo.com/events/show/202064487892

Unknown end tag for &lt;/guid&gt;

 <pubDate>Thu, 13 Aug 2009 00:54:10 +0100

Unknown end tag for &lt;/pubDate&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:   ```
<nowiki><title>Tyson Key posted on Twitter

Unknown end tag for &lt;/title&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:    ```
<nowiki><link>http://www.plaxo.com/events/show/202064487892

Unknown end tag for &lt;/link&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:    ```
<nowiki><description><![CDATA[@<a href="http://twitter.com/symbian_markw" target="_blank">symbian_markw

Unknown end tag for &lt;/a&gt;

 It's all about the architecture. 'Nuff said...<p><a href="http://twitter.com/vmlemon/statuses/3275771117" target="_blank">more &raquo;

Unknown end tag for &lt;/a&gt;



Unknown end tag for &lt;/p&gt;

]]>

Unknown end tag for &lt;/description&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:    ```
<nowiki><author><![CDATA[Tyson Key]]>

Unknown end tag for &lt;/author&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:
:    ```
<nowiki><plaxoPulse:pubDateUnix>1250121250

Unknown end tag for &lt;/pubDateUnix&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:    ```
<nowiki><plaxoPulse:lastModified>2009-08-12 16:54:10

Unknown end tag for &lt;/lastModified&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:    ```
<nowiki><plaxoPulse:authorProfile>http://www.plaxo.com/profile/show/201864723191?pk=b7694d3b3b9d9fa6de40cd0d462d4d1607f4069d

Unknown end tag for &lt;/authorProfile&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:```
<nowiki><plaxoPulse:feedIcon>Twitter.gif

Unknown end tag for &lt;/feedIcon&gt;



Unknown end tag for &lt;/nowiki&gt;

```
::    ```
<nowiki><plaxoPulse:authorPhoto>

Unknown end tag for &lt;/authorPhoto&gt;



Unknown end tag for &lt;/nowiki&gt;

```
::    ```
<nowiki><plaxoPulse:numComments>0

Unknown end tag for &lt;/numComments&gt;



Unknown end tag for &lt;/nowiki&gt;

```
::    ```
<nowiki><plaxoPulse:numViews>0

Unknown end tag for &lt;/numViews&gt;



Unknown end tag for &lt;/nowiki&gt;

```
:
::    ```
<nowiki>

Unknown end tag for &lt;/item&gt;



Unknown end tag for &lt;/nowiki&gt;

 ```


**It may be interesting to support the**```
numViews``` (object view count), ```
numComments``` (object comment count) and ```
feedIcon``` (feed favicon) attributes in the OpenStream specification. The ```
feedIcon``` attribute may also be a worthy method of supporting [FriendFeed](http://www.friendfeed.com) service icon metadata.

### Jaiku RSS Extensions ###
**[Jaiku](http://www.jaiku.com) is a microblogging service provided by [Google, Inc.](http://www.google.com)**

### Wakoopa RSS Extensions ###
[Wakoopa](http://www.wakoopa.com) is a [last.fm](http://last.fm)-style social network and logging system for software.