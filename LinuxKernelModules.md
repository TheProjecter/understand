http://www.cyberciti.biz/tips/build-linux-kernel-module-against-installed-kernel-source-tree.html

http://code.google.com/p/understand/source/browse/trunk/usr/src/linux-source-3.0.0/linux-source-3.0.0/drivers/fakelb.c

http://comments.gmane.org/gmane.linux.network.zigbee.devel/903

https://wiki.ubuntu.com/KernelCustomBuild

http://wiki.cchtml.com/index.php/Ubuntu_Dapper_Installation_Guide#Problems_with_module-assistant

## Build the `fakehard` 802.15.4 driver under Ubuntu ##

root@UmBongo:/usr/src/linux-source-3.0.0/linux-source-3.0.0/drivers/ieee802154#

```


#obj-$(CONFIG_IEEE802154_FAKEHARD) += fakehard.o

obj-m += fakehard.o

ccflags-y := -DDEBUG -DCONFIG_FFD

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
 
```

`cp fakehard.ko /lib/modules/3.0.0-14-generic/extra/`
`depmod -a`

## ZigBee notes ##
http://sourceforge.net/apps/trac/linux-zigbee/wiki/GettingStarted-0.2

```
iz listphy
wpan-phy0  IEEE 802.15.4 PHY object
    page: 0  channel: n/a
    channels on page 0: 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26
    channels on page 3: 0 1 2 3 4 5 6 7 8 9 10 11 12 13

```

## AppleTalk/LocalTalk COPS ##

root@UmBongo:/usr/src/linux-source-3.0.0/linux-source-3.0.0/drivers/net/appletalk#

```
#
# Makefile for drivers/net/appletalk
#

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

obj-m += ipddp.o cops.o ltpc.o

obj-$(CONFIG_IPDDP) += ipddp.o
obj-$(CONFIG_COPS) += cops.o
obj-$(CONFIG_LTPC) += ltpc.o
```