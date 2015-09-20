# Introduction #

Add your content here.

## Linux (x86) Dialler ##

## AT Commands ##
The MF627 utilises a number of non-standard, proprietary AT commands, in additional to documented standard AT commands to perform certain functions. These are listed in the table below, in no specific order, along with an attempt to provide examples and descriptions:
|<b>AT Command</b>|<b>Example Usage</b>|<b>Expected Result</b>|<b>Description</b>|
|:----------------|:-------------------|:---------------------|:-----------------|
|`AT+CIMI`        |`AT+CIMI`           |Returns a result similar to:<br><code>234201201366409</code><br /><br /><code>OK</code><table><thead><th>Returns the <a href='http://en.wikipedia.org/wiki/International_Mobile_Subscriber_Identity'>International Mobile Subscriber Identity</a> (IMSI), maybe correlating with ITU E.212.<br />Read this as <code>Country ID</code>, <code>Operator ID</code> and <code>Opaque 10-Digit ID</code>.<br /> In the case of the example, this is <code>Country ID</code>: <code>234</code> (United Kingdom), <code>Operator ID</code>: <code>20</code> (Hutchison 3G UK, Ltd.), and the <code>Opaque 10-Digit ID</code>.</th></thead><tbody>
<tr><td><code>AT+CSQ</code></td><td><code>AT+CSQ</code> </td><td>Returns a result similar to:<br /> <code>+CSQ: 12,99</code><br /><br /><code>OK</code></td><td>...               </td></tr>
<tr><td><code>AT+ZPAS?</code></td><td><code>AT+ZPAS?</code></td><td>Returns a result similar to one of the following, depending on network and baseband state: <br /><code>+ZPAS: "HSDPA","CS_PS"</code><br /><br /><code>OK</code><br /><br /><br /><code>+ZPAS: "3G","CS_PS"</code><br /><br /><code>OK</code></td></tr>
<tr><td><code>AT+ZDON?</code></td><td>...                 </td><td><code>+ZDON: "3",234,20,"ROAM_OFF"</code></td></tr></tbody></table>

Some additional information of interest is available <a href='http://www.anotherurl.com/library/at_test.htm'>here</a>.<br>
<br>
<h2>USB</h2>
<ul><li>Reported in <code>lspci</code> as <code>Bus 002 Device 105: ID 19d2:0031 ONDA Communication S.p.A.</code>
</li><li>The device has multiple modes of operation (default state is an emulated USB/SCSI CD-ROM drive that must be "ejected" in order to switch to modem mode)