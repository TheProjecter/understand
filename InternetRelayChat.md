## Specifications and Implementations ##
  * The IRC protocol is documented in [Request for Comments (RFC) Document #1459](http://www.faqs.org/rfcs/rfc1459.html)
  * There are a vast number of client and server implementations of it available (too many to sanely list here), including the clients listed [here](http://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients), a number of non-human-clients ("robots"), and preconfigured IRC networks and services (e.g. [FreeNode](http://www.freenode.org))
  * Additional information is available at [Wikipedia](http://en.wikipedia.org/wiki/Internet_Relay_Chat)

## Initial Handshake Example ##
### With NetCat-based "Server" and Pidgin ###
|<b>Verb and Arguments</b>|<b>Description</b>|
|:------------------------|:-----------------|
|`USER Username nagasaki.home localhost :Real Name`|Specifies username, connection originator hostname, destination hostname and "real name"|
|`NICK Username`          |Specifies nickname/handle (often same as username)|
|`QUIT :Leaving.`         |Finish up by leaving the server with the message "Leaving." without quotes|

## Microsoft Comic Chat ##
### Brief Background and Obtaining the Client ###
  * A copy of the client for Windows is still available, [here](http://mermeliz.com/cchat.htm)
  * Some of the extensions used are documented in a series of four Internet Drafts ([00](http://tools.ietf.org/id/draft-pfenning-irc-extensions-00.txt), [01](http://tools.ietf.org/id/draft-pfenning-irc-extensions-01.txt), [02](http://tools.ietf.org/id/draft-pfenning-irc-extensions-02.txt) and [04](http://tools.ietf.org/id/draft-pfenning-irc-extensions-04.txt) - 03 was never released), at the linked URLs
  * A copy of these Internet Drafts will also be mirrored here, in case they ever disappear from the IETF website

### Version and Identification ###