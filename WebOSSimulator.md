## Getting CaDAVer Running ##
The "easiest" (subjective) way to run CaDAVer is to copy the `/usr/bin/cadaver` executable, and the listed shared objects to a directory available to a local HTTP server (e.g. Apache), and then use BusyBox's internal `wget` command under `novaterm` to download them.

Within the WebOS VirtualBox virtual machine, the host system's IPv4 address is `10.0.2.2`, and the guest's is `10.0.2.15`, although traffic intended for the host only, masquerades as traffic from `127.0.0.1` and is visible on the loopback interface.

### Dependencies ###
As copied from a Fedora 10 installation, the following additional shared libraries are required (these must be placed in `/lib` on the simulator), in order to get CaDAVer to function:

  * `libreadline.so.5` (`/lib/libreadline.so.5.2`)
  * `libneon.so.27` (`/usr/lib/libneon.so.27.1.3`)
  * `libtinfo.so.5` (`/lib/libtinfo.so.5.6`)
  * `libgnutls.so.26` (`/usr/lib/libgnutls.so.26.4.6`)
  * `libpakchois.so.0` (`/usr/lib/libpakchois.so.0.1.0`)
  * `libgssapi_krb5.so.2` (`/usr/lib/libgssapi_krb5.so.2.2`)
  * `libkrb5.so.3` (`/usr/lib/libkrb5.so.3.3`)
  * `libk5crypto.so.3` (`/usr/lib/libk5crypto.so.3.1`)
  * `libexpat.so.1`) (`/lib/libexpat.so.1.5.2`)
  * `libtasn1.so.3` (`/usr/lib/libtasn1.so.3.0.16`)
  * `libkrb5support.so.0` (`/usr/lib/libkrb5support.so.0.1`)
  * `libkeyutils.so.1` (`/lib/libkeyutils-1.2.so`)
  * `libselinux.so.1` (`lib/libselinux.so.1`)

### Current Outcome ###
At present, after copying the dependencies, the following error message is produced whilst trying to run the `cadaver` binary:<br />
``./cadaver: /lib/libc.so.6: version `GLIBC_2.8' not found (required by /lib/libgnutls.so.26)``<br />
``./cadaver: /lib/libc.so.6: version `GLIBC_2.7' not found (required by /lib/libkrb5support.so.0)``<br />
``./cadaver: /lib/libc.so.6: version `GLIBC_2.8' not found (required by /lib/libselinux.so.1)``