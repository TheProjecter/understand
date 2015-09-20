## Detecting the Presence of the HTTPMail Extensions ##
According to [MS-XWDMAIL](http://msdn.microsoft.com/en-us/library/dd299450(v=exchg.80).aspx), a server is supposed to send an `Allow-Extension` HTTP header containing the value `urn:schemas:httpmail` with the output of the `OPTIONS` verb.

## Potential Non-Code Intrusive Hacks/Workarounds ##
Add `Header append Allow-Extension urn:schemas:httpmail` or `Header add Allow-Extension urn:schemas:httpmail` to permanently switch on the HTTPMail extension notice, at the cost of potentially violating the spec or upsetting clients. According to the specification, it is also necessary to send a `Public-Extension` header containing the same value as `Allow-Extension`, prior to that header.`

## Error Messages ##
Outlook Express, with `Allow-Extension` Header:
`Unable to poll for new messages on your HTTP server.  Account: 'http://10.0.2.2:8008', Server: 'http://10.0.2.2:8008/', Protocol: HTTPMail, Port: 0, Secure(SSL): No, Error Number: 0x80042007`

Outlook 2003, with `Allow-Extension` Header:
`Task 'http://10.0.2.2:8008: Folder:Inbox Downloading all items.' reported error (0x800CCCF4) : 'An unknown error has occurred. Please save any existing work and restart the program.'`

## A Server Without the Extensions ##
Server used: `Apache/2.2.11 (Fedora) DAV/2 PHP/5.2.9 mod_python/3.3.1 Python/2.5.2 mod_ssl/2.2.11 OpenSSL/0.9.8g SVN/1.5.4 mod_perl/2.0.4 Perl/v5.10.0` operating on TCP port 8008, serving WebDAV with SVN extensions - HTTP Authentication is enabled, using the username "Administrator" and no password.

Client 1: `Outlook-Express/6.0 (MSIE 6.0; Windows NT 5.0; TmstmpExt)`

## Initial HTTP Stream from Client 1 ##
Sent by Client:
<img src='http://understand.googlecode.com/svn/wiki/OEOutboundFlow1.png' /><br />
Received from Server:
<img src='http://understand.googlecode.com/svn/wiki/OEInboundFlow1.png' /><br />
Sent by Client:
<img src='http://understand.googlecode.com/svn/wiki/OEOutboundFlow2.png' /><br />
Received from Server:
<img src='http://understand.googlecode.com/svn/wiki/OEInboundFlow3.png' /><br />