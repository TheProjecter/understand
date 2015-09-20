## Interpreting the Examples ##
**Colour Codes:**
|<b>Client-Side</b>|<b>Server-Side</b>|
|:-----------------|:-----------------|
|<font color='green'><code>Green</code></font>|<font color='orange'><code>Orange</code></tbody></table>

<h2>Example Exchanges ##
## Apache 2.2.x and Nokia S60 5th Edition Remote Storage ##
The `User-Agent` string for the Remote Client implementation is `S60 Remote Storage WebDav client`. The Client expects that the server implementation supports the `LOCK` and `UNLOCK` HTTP verbs, which are always available on "plain" Apache 2.2 WebDAV volumes even without authentication, but not on SVN WebDAV volumes (use of HTTP Authentication and the `mod_dav_lock` Apache module are mandatory in this case).

### Apache 2.2.x and CaDAVer 0.23.2/libneon 0.28.3 ###
The version used for these examples is `Apache/2.2.11 (Fedora) DAV/2 PHP/5.2.9 mod_python/3.3.1 Python/2.5.2 mod_ssl/2.2.11 OpenSSL/0.9.8g mod_perl/2.0.4 Perl/v5.10.0`..

The `User-Agent` string used for the CaDAVer version in this example is `cadaver/0.23.2 neon/0.28.3`.

Connecting to the server and listing the empty `/` directory:

<font color='green'>
<code>OPTIONS / HTTP/1.1</code><br />
<code>Host: localhost:8008</code><br />
<code>User-Agent: cadaver/0.23.2 neon/0.28.3</code><br />
<code>Keep-Alive: </code><br />
<code>Connection: TE, Keep-Alive</code><br />
<code>TE: trailers</code><br />
</font>

<font color='orange'>
<code>HTTP/1.1 200 OK</code><br />
<code>Date: Sat, 11 Jul 2009 12:49:22 GMT</code><br />
<code>Server: Apache/2.2.11 (Fedora) DAV/2 PHP/5.2.9 mod_python/3.3.1 Python/2.5.2 mod_ssl/2.2.11 OpenSSL/0.9.8g mod_perl/2.0.4 Perl/v5.10.0</code><br />
<code>DAV: 1,2</code><br />
<code>DAV: &lt;http://apache.org/dav/propset/fs/1&gt;</code><br />
<code>MS-Author-Via: DAV</code><br />
<code>Allow: OPTIONS,GET,HEAD,POST,DELETE,TRACE,PROPFIND,PROPPATCH,COPY,MOVE,LOCK,UNLOCK</code><br />
<code>Content-Length: 0</code><br />
<code>Keep-Alive: timeout=15, max=100</code><br />
<code>Connection: Keep-Alive</code><br />
<code>Content-Type: httpd/unix-directory</code>
</font>

<font color='green'>
<code>PROPFIND / HTTP/1.1</code><br />
<code>Host: localhost:8008</code><br />
<code>User-Agent: cadaver/0.23.2 neon/0.28.3</code><br />
<code>Connection: TE</code><br />
<code>TE: trailers</code><br />
<code>Depth: 0</code><br />
<code>Content-Length: 288</code><br />
<code>Content-Type: application/xml</code><br />
<code>&lt;?xml version="1.0" encoding="utf-8"?&gt;</code><br />
<code>&lt;propfind xmlns="DAV:"&gt;&lt;prop&gt;</code><br />
<code>&lt;getcontentlength xmlns="DAV:"/&gt;</code><br />
<code>&lt;getlastmodified xmlns="DAV:"/&gt;</code><br />
<code>&lt;executable xmlns="http://apache.org/dav/props/"/&gt;</code><br />
<code>&lt;resourcetype xmlns="DAV:"/&gt;</code><br />
<code>&lt;checked-in xmlns="DAV:"/&gt;</code><br />
<code>&lt;checked-out xmlns="DAV:"/&gt;</code><br />
<code>&lt;/prop&gt;&lt;/propfind&gt;</code><br />