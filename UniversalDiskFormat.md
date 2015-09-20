## References/More Information ##
  * The current steward/maintainer of the UDF specifications is the [Optical Storage Technology Association (OSTA)](http://www.osta.org), who currently make them freely available [here](http://www.osta.org/specs/) as PDF files
  * Some information on various implementations is curated on the [UDFInteroperabilityTesting](UDFInteroperabilityTesting.md) page of this wiki
  * Additional factoids and information on UDF are also available over at [Wikipedia](http://en.wikipedia.org/wiki/Universal_Disk_Format)

## Useful Tools ##
### UDFClient ###
  * [UDFClient](http://www.13thmonkey.org/udfclient) includes a tool (`udfdump`) to print the structures of a UDF volume - requires BSD Make (AKA `bmake`) on some systems)
  * For best results when using a disk-based file, instead of a device node attached to a physical drive, invoke `udfdump` using the arguments `-u 3 -S`
  * It may also be a good idea to specify the block size using `-b 512`, for example