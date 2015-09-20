## Obtaining BeOS [R3](https://code.google.com/p/understand/source/detail?r=3).1 executables/libraries ##
Libraries necessary for running BeOS [R3](https://code.google.com/p/understand/source/detail?r=3).1 executables are available from `/beos/system/lib`, on the "`BeOS Intel R3.1`" volume of [Track02.iso](http://www.theoldcomputer.com/roms/getfile.php?file=Li9QQy8vT3BlcmF0aW5nLVN5c3RlbXMvQmVPUy9CZU9TIDMuMSAoQkEpLnJhcg==). This can be mounted successfully under a build of Haiku.

## Running under WINE ##

### Before adding `libroot.so` ###
```
tyson@tyson-VirtualBox:/mnt/hgfs/Documents/Desktop/BinUtils$ wine fileb3.exe 
wine: created the configuration directory '/home/tyson/.wine'
fixme:storage:create_storagefile Storage share mode not implemented.
err:mscoree:LoadLibraryShim error reading registry key for installroot
err:mscoree:LoadLibraryShim error reading registry key for installroot
err:mscoree:LoadLibraryShim error reading registry key for installroot
err:mscoree:LoadLibraryShim error reading registry key for installroot
err:mscoree:LoadLibraryShim error reading registry key for installroot
err:mscoree:LoadLibraryShim error reading registry key for installroot
fixme:iphlpapi:NotifyAddrChange (Handle 0xfce8ac, overlapped 0xfce890): stub
wine: configuration in '/home/tyson/.wine' has been updated.
err:module:import_dll Library libroot.so (which is needed by L"Z:\\mnt\\hgfs\\Documents\\Desktop\\BinUtils\\fileb3.exe") not found
err:module:LdrInitializeThunk Main exe initialization for L"Z:\\mnt\\hgfs\\Documents\\Desktop\\BinUtils\\fileb3.exe" failed, status c0000135
```

### After adding `libroot.so` ###
```
wine: Unhandled page fault on read access to 0xffffffff at address 0x348c8b (thread 0009), starting debugger...
fixme:dbghelp_dwarf:dwarf2_parse_subprogram Unhandled Tag type 0x26 at ctx(0x33c19c,L"libc.so.6"), for debug_info(abbrev:0x4403a0,symt:0x4ec678)
fixme:dbghelp_dwarf:compute_location Only supporting one reg (edx/19 -> -2)
fixme:dbghelp_dwarf:compute_location Only supporting one reg (edx/19 -> -2)
fixme:dbghelp_dwarf:compute_location Only supporting one reg (edx/19 -> -2)
fixme:dbghelp_dwarf:compute_location Only supporting one reg (edx/19 -> -2)
fixme:dbghelp_dwarf:dwarf2_parse_subprogram Unhandled Tag type 0x26 at ctx(0x33c19c,L"libc.so.6"), for debug_info(abbrev:0xf00f4c,symt:0x1232464)
fixme:dbghelp_dwarf:dwarf2_parse_subprogram_block Unhandled Tag type 0xf at ctx(0x33c19c,L"libc.so.6"), for debug_info(abbrev:0xf00ffc,symt:(nil))
fixme:dbghelp_dwarf:dwarf2_parse_subprogram_block Unhandled Tag type 0xf at ctx(0x33c19c,L"libc.so.6"), for debug_info(abbrev:0xf00ffc,symt:(nil))
fixme:dbghelp_dwarf:dwarf2_parse_subprogram_block Unhandled Tag type 0x26 at ctx(0x33c19c,L"libc.so.6"), for debug_info(abbrev:0x1480c1c,symt:(nil))
```

The backtrace looks like:
```
Unhandled exception: page fault on read access to 0xffffffff in 32-bit code (0x00348c8b).
Register dump:
 CS:0073 SS:007b DS:007b ES:007b FS:0033 GS:003b
 EIP:00348c8b ESP:0032fa1c EBP:0032fe40 EFLAGS:00010246(  R- --  I  Z- -P- )
 EAX:0000002f EBX:00000000 ECX:6f3f81d7 EDX:0037d364
 ESI:bfcc6e14 EDI:00000000
Stack dump:
0x0032fa1c:  80003e23 00000000 00000000 00000000
0x0032fa2c:  00000000 00000000 00000000 00000000
0x0032fa3c:  00000000 00000000 00000000 00000000
0x0032fa4c:  00000000 00000000 00000000 00000000
0x0032fa5c:  00000000 00000000 00000000 00000000
0x0032fa6c:  00000000 00000000 00000000 00000000
Backtrace:
=>0 0x00348c8b in libroot.so (+0x18c8b) (0x0032fe40)
  1 0x7b861d48 call_process_entry+0xb() in kernel32 (0x0032fe58)
  2 0x7b861e8d call_process_entry+0x150() in kernel32 (0x0032fea8)
  3 0x7bc7edfc call_thread_func_wrapper+0xb() in ntdll (0x0032feb8)
  4 0x7bc7ee4b call_thread_func+0x44() in ntdll (0x0032ff98)
  5 0x7bc7edda in ntdll (+0x6edd9) (0x0032ffb8)
  6 0x7bc545bf in ntdll (+0x445be) (0x0032ffe8)
  7 0xb7657b5d wine_call_on_stack+0x1c() in libwine.so.1 (0x00000000)
  8 0xb7657b3b wine_switch_to_stack+0x2a() in libwine.so.1 (0xbfcc6e38)
  9 0x7bc54901 LdrInitializeThunk+0x341() in ntdll (0xbfcc6eb8)
  10 0x7b862766 __wine_kernel_init+0x719() in kernel32 (0xbfcc7d48)
  11 0x7bc5507b __wine_process_init+0x156() in ntdll (0xbfcc7d98)
  12 0xb76563ce wine_init+0x140() in libwine.so.1 (0xbfcc7dd8)
  13 0x7bf011c6 main+0x13d() in <wine-loader> (0xbfcc8218)
  14 0xb7485905 __libc_start_main+0xf4(main=0x7bf01088, argc=0x2, ubp_av=0xbfcc82b4, init=0x7bf011f0, fini=0x7bf01260, rtld_fini=0xb77a45f0, stack_end=0xbfcc82ac) [/build/buildd/eglibc-2.17/csu/libc-start.c:260] in libc.so.6 (0x00000000)
0x00348c8b: int﻿  $0x25
Modules:
Module﻿  Address﻿  ﻿  ﻿  Debug info﻿  Name (20 modules)
ELF﻿    330000-  390000﻿  Export          libroot.so
ELF﻿  7b800000-7ba43000﻿  Dwarf           kernel32<elf>
  \-PE﻿  7b810000-7ba43000﻿  \               kernel32
ELF﻿  7bc00000-7bce3000﻿  Dwarf           ntdll<elf>
  \-PE﻿  7bc10000-7bce3000﻿  \               ntdll
ELF﻿  7bf00000-7bf04000﻿  Dwarf           <wine-loader>
ELF﻿  7ed28000-7ed4a000﻿  Deferred        libtinfo.so.5
ELF﻿  7ed4a000-7ed6f000﻿  Deferred        libncurses.so.5
ELF﻿  7ef82000-7ef8f000﻿  Deferred        libnss_files.so.2
ELF﻿  7ef8f000-7ef9b000﻿  Deferred        libnss_nis.so.2
ELF﻿  7ef9b000-7efb4000﻿  Deferred        libnsl.so.1
ELF﻿  7efb4000-7efbd000﻿  Deferred        libnss_compat.so.2
ELF﻿  7efbd000-7f000000﻿  Deferred        libm.so.6
PE﻿  80000000-8000a000﻿  Deferred        fileb3
ELF﻿  b7467000-b746c000﻿  Deferred        libdl.so.2
ELF﻿  b746c000-b7620000﻿  Dwarf           libc.so.6
ELF﻿  b7621000-b763c000﻿  Deferred        libpthread.so.0
ELF﻿  b764f000-b7793000﻿  Dwarf           libwine.so.1
ELF﻿  b7795000-b77b7000﻿  Deferred        ld-linux.so.2
ELF﻿  b77b7000-b77b8000﻿  Deferred        [vdso].so
Threads:
process  tid      prio (all id:s are in hex)
00000008 (D) Z:\mnt\hgfs\Documents\Desktop\BinUtils\fileb3.exe
﻿  00000009    0 <==
0000000e services.exe
﻿  00000020    0
﻿  0000001f    0
﻿  00000019    0
﻿  00000018    0
﻿  00000017    0
﻿  00000015    0
﻿  00000010    0
﻿  0000000f    0
00000012 winedevice.exe
﻿  0000001d    0
﻿  0000001a    0
﻿  00000014    0
﻿  00000013    0
0000001b plugplay.exe
﻿  00000021    0
﻿  0000001e    0
﻿  0000001c    0
00000022 explorer.exe
﻿  00000023    0
System information:
    Wine build: wine-1.4.1
    Platform: i386
    Host system: Linux
    Host version: 3.11.0-12-generic
```