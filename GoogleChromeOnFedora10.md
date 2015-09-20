## Converted Packages ##
  * Currently, a version of the Debian package available [here](http://www.google.com/chrome/intl/en/eula_dev.html?dl=unstable_i386_deb) converted to an RPM that seems to install without errors is available [here](http://house404.co.uk/google-chrome-unstable-3.0.183.1-1.i386.rpm)


## Required Shared Libraries ##

It is necessary to create symbolic links for several libraries, before Chrome will run, these are as follows:
  * `/usr/lib/libnss3.so` -> `/usr/lib/libnss3.so.1d`
  * `/usr/lib/libnssutil3.so` -> `libnssutil3.so.1d`
  * `/usr/lib/libsmime3.so` -> `/usr/lib/libsmime3.so.1d`
  * `/usr/lib/libssl3.so` -> `/usr/lib/libssl3.so.1d`
  * `/usr/lib/libplds4.so` -> `/usr/lib/libplds4.so.0d`
  * `/usr/lib/libplc4.so` -> `/usr/lib/libplc4.so.0d`
  * `/usr/lib/libnspr4.so` -> `/usr/lib/libnspr4.so.0d`