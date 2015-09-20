# SkyOS PE/COFF executables #

For some time, SkyOS used to use PE as its native executable format, and some folks from the ReactOS project managed to sort-of get a SkyOS running using a [small shim](https://code.google.com/p/reactos-mirror/source/detail?spec=svn10514&r=10501) library.
# BeOS [R3](https://code.google.com/p/understand/source/detail?r=3) PE/COFF executables #

A rare example of a BeOS PE/COFF executable, containing a port of the GNU `file` utility is [available](http://hyperlogos.org/files/gnufile-3.20.1.beos-src.tgz).

## `objdump -x` Output (`file`) ##
```

fileb3.exe:     file format pei-i386
fileb3.exe
architecture: i386, flags 0x0000010b:
HAS_RELOC, EXEC_P, HAS_DEBUG, D_PAGED
start address 0x80003df0

Characteristics 0x10e
	executable
	line numbers stripped
	symbols stripped
	32 bit words

Time/Date		Sat Apr 11 18:20:25 1998
Magic			010b	(PE32)
MajorLinkerVersion	2
MinorLinkerVersion	50
SizeOfCode		00003000
SizeOfInitializedData	00001e00
SizeOfUninitializedData	00000200
AddressOfEntryPoint	00003df0
BaseOfCode		00001000
BaseOfData		00004000
ImageBase		80000000
SectionAlignment	00001000
FileAlignment		00000200
MajorOSystemVersion	1
MinorOSystemVersion	0
MajorImageVersion	0
MinorImageVersion	0
MajorSubsystemVersion	4
MinorSubsystemVersion	0
Win32Version		00000000
SizeOfImage		0000a000
SizeOfHeaders		00000400
CheckSum		00000000
Subsystem		00000000	(unspecified)
DllCharacteristics	00000000
SizeOfStackReserve	00100000
SizeOfStackCommit	00001000
SizeOfHeapReserve	00100000
SizeOfHeapCommit	00001000
LoaderFlags		00000000
NumberOfRvaAndSizes	00000010

The Data Directory
Entry 0 00008000 0000005f Export Directory [.edata (or where ever we found it)]
Entry 1 00007000 0000058f Import Directory [parts of .idata]
Entry 2 00000000 00000000 Resource Directory [.rsrc]
Entry 3 00000000 00000000 Exception Directory [.pdata]
Entry 4 00000000 00000000 Security Directory
Entry 5 00009000 000005a8 Base Relocation Directory [.reloc]
Entry 6 00000000 00000000 Debug Directory
Entry 7 00000000 00000000 Description Directory
Entry 8 00000000 00000000 Special Directory
Entry 9 00000000 00000000 Thread Storage Directory [.tls]
Entry a 00000000 00000000 Load Configuration Directory
Entry b 00000000 00000000 Bound Import Directory
Entry c 00000000 00000000 Import Address Table Directory
Entry d 00000000 00000000 Delay Import Directory
Entry e 00000000 00000000 CLR Runtime Header
Entry f 00000000 00000000 Reserved

There is an import table in .idata at 0x80007000

The Import Tables (interpreted .idata section contents)
 vma:            Hint    Time      Forward  DLL       First
                 Table   Stamp     Chain    Name      Thunk
 00007000	00007028 00000000 00000000 00007584 00007138

	DLL Name: libroot.so
	vma:  Hint/Ord Member-Name Bound-To
	7248	  693  strrchr
	7254	  478  getenv
	725e	  204  _files
	7268	  429  fprintf
	7274	  402  exit
	727c	  571  optarg
	7286	  486  getopt
	7290	  573  optind
	729a	  687  strlen
	72a4	  680  strcmp
	72ae	  426  fopen
	72b8	  202  _errnop
	72c4	  685  strerror
	72d0	  416  fgets
	72da	  620  rewind
	72e4	  408  fclose
	72ee	  188  __swap_int32
	72fe	  460  fstat
	7308	  586  printf
	7312	  157  __put_char
	7320	  569  open
	7328	  595  read
	7330	  180  __rt_sltoi64
	7340	  543  lseek
	734a	  160  __rt_cmps64
	735a	  737  utime
	7364	  365  close
	736e	  317  _stack_alloc
	737e	  351  calloc
	7388	  545  malloc
	7392	  682  strcpy
	739c	  679  strchr
	73a6	  433  free
	73ae	  608  realloc
	73ba	  557  memset
	73c4	  701  strtoul
	73d0	  123  __ctype_map
	73e0	  726  tolower
	73ec	  690  strncmp
	73f8	  430  fputc
	7402	  544  lstat
	740c	  674  stat
	7414	  605  readlink
	7420	  678  strcat
	742a	  376  ctime
	7434	  553  memchr
	743e	  698  strtok
	7448	  554  memcmp
	7452	  580  pipe
	745a	  427  fork
	7462	  388  dup
	746a	  401  execvp
	7474	  747  write
	747e	  742  wait
	7486	  431  fputs
	7490	  739  vfprintf
	749c	  413  fflush
	74a6	  117  _RegisterExceptionTables
	74c2	  119  _UnRegisterExceptionTables
	74e0	  335  argv_save
	74ee	  392  environ
	74fa	  421  find_thread
	750a	  153  __main_thread_id
	751e	  244  _kget_thread_stacks_
	7536	  197  _data_offset_main_
	754c	  193  _call_init_routines_
	7564	  321  _thread_do_exit_notification

 00007014	00000000 00000000 00000000 00000000 00000000

There is an export table in .edata at 0x80008000

The Export Tables (interpreted .edata section contents)

Export Flags 			0
Time/Date stamp 		352fa659
Major/Minor 			0/0
Name 				0000803c file
Ordinal Base 			1
Number in:
	Export Address Table 		00000002
	[Name Pointer/Ordinal] Table	00000002
Table Addresses
	Export Address Table 		00008028
	Name Pointer Table 		00008030
	Ordinal Table 			00008038

Export Address Table -- Ordinal Base 1
	[   0] +base[   1] 3dbe Export RVA
	[   1] +base[   2] 3dd7 Export RVA

[Ordinal/Name Pointer] Table
	[   0] _init_routine_
	[   1] _term_routine_


PE File Base Relocations (interpreted .reloc section contents)

Virtual Address: 00001000 Chunk size 424 (0x1a8) Number of fixups 208
	reloc    0 offset   24 [1024] HIGHLOW
	reloc    1 offset   2c [102c] HIGHLOW
	reloc    2 offset   36 [1036] HIGHLOW
	reloc    3 offset   3f [103f] HIGHLOW
	reloc    4 offset   44 [1044] HIGHLOW
	reloc    5 offset   4a [104a] HIGHLOW
	reloc    6 offset   52 [1052] HIGHLOW
	reloc    7 offset   60 [1060] HIGHLOW
	reloc    8 offset   64 [1064] HIGHLOW
	reloc    9 offset   b2 [10b2] HIGHLOW
	reloc   10 offset   b7 [10b7] HIGHLOW
	reloc   11 offset   bc [10bc] HIGHLOW
	reloc   12 offset   c8 [10c8] HIGHLOW
	reloc   13 offset   de [10de] HIGHLOW
	reloc   14 offset   eb [10eb] HIGHLOW
	reloc   15 offset   fe [10fe] HIGHLOW
	reloc   16 offset  10b [110b] HIGHLOW
	reloc   17 offset  120 [1120] HIGHLOW
	reloc   18 offset  127 [1127] HIGHLOW
	reloc   19 offset  12e [112e] HIGHLOW
	reloc   20 offset  136 [1136] HIGHLOW
	reloc   21 offset  140 [1140] HIGHLOW
	reloc   22 offset  14a [114a] HIGHLOW
	reloc   23 offset  163 [1163] HIGHLOW
	reloc   24 offset  169 [1169] HIGHLOW
	reloc   25 offset  16e [116e] HIGHLOW
	reloc   26 offset  17a [117a] HIGHLOW
	reloc   27 offset  185 [1185] HIGHLOW
	reloc   28 offset  193 [1193] HIGHLOW
	reloc   29 offset  1a6 [11a6] HIGHLOW
	reloc   30 offset  1af [11af] HIGHLOW
	reloc   31 offset  1c1 [11c1] HIGHLOW
	reloc   32 offset  1c7 [11c7] HIGHLOW
	reloc   33 offset  1cc [11cc] HIGHLOW
	reloc   34 offset  1d8 [11d8] HIGHLOW
	reloc   35 offset  1e3 [11e3] HIGHLOW
	reloc   36 offset  1ef [11ef] HIGHLOW
	reloc   37 offset  1fc [11fc] HIGHLOW
	reloc   38 offset  213 [1213] HIGHLOW
	reloc   39 offset  225 [1225] HIGHLOW
	reloc   40 offset  22d [122d] HIGHLOW
	reloc   41 offset  256 [1256] HIGHLOW
	reloc   42 offset  25c [125c] HIGHLOW
	reloc   43 offset  269 [1269] HIGHLOW
	reloc   44 offset  278 [1278] HIGHLOW
	reloc   45 offset  27f [127f] HIGHLOW
	reloc   46 offset  28e [128e] HIGHLOW
	reloc   47 offset  296 [1296] HIGHLOW
	reloc   48 offset  2a0 [12a0] HIGHLOW
	reloc   49 offset  2b7 [12b7] HIGHLOW
	reloc   50 offset  2d8 [12d8] HIGHLOW
	reloc   51 offset  2e6 [12e6] HIGHLOW
	reloc   52 offset  2f8 [12f8] HIGHLOW
	reloc   53 offset  326 [1326] HIGHLOW
	reloc   54 offset  334 [1334] HIGHLOW
	reloc   55 offset  380 [1380] HIGHLOW
	reloc   56 offset  3fa [13fa] HIGHLOW
	reloc   57 offset  400 [1400] HIGHLOW
	reloc   58 offset  416 [1416] HIGHLOW
	reloc   59 offset  423 [1423] HIGHLOW
	reloc   60 offset  42b [142b] HIGHLOW
	reloc   61 offset  434 [1434] HIGHLOW
	reloc   62 offset  439 [1439] HIGHLOW
	reloc   63 offset  446 [1446] HIGHLOW
	reloc   64 offset  452 [1452] HIGHLOW
	reloc   65 offset  45b [145b] HIGHLOW
	reloc   66 offset  46b [146b] HIGHLOW
	reloc   67 offset  471 [1471] HIGHLOW
	reloc   68 offset  47c [147c] HIGHLOW
	reloc   69 offset  49e [149e] HIGHLOW
	reloc   70 offset  4bb [14bb] HIGHLOW
	reloc   71 offset  4c9 [14c9] HIGHLOW
	reloc   72 offset  4dc [14dc] HIGHLOW
	reloc   73 offset  4fa [14fa] HIGHLOW
	reloc   74 offset  505 [1505] HIGHLOW
	reloc   75 offset  51e [151e] HIGHLOW
	reloc   76 offset  529 [1529] HIGHLOW
	reloc   77 offset  537 [1537] HIGHLOW
	reloc   78 offset  53f [153f] HIGHLOW
	reloc   79 offset  54b [154b] HIGHLOW
	reloc   80 offset  550 [1550] HIGHLOW
	reloc   81 offset  57b [157b] HIGHLOW
	reloc   82 offset  58b [158b] HIGHLOW
	reloc   83 offset  593 [1593] HIGHLOW
	reloc   84 offset  59c [159c] HIGHLOW
	reloc   85 offset  5ad [15ad] HIGHLOW
	reloc   86 offset  5b8 [15b8] HIGHLOW
	reloc   87 offset  5d9 [15d9] HIGHLOW
	reloc   88 offset  6b5 [16b5] HIGHLOW
	reloc   89 offset  6cd [16cd] HIGHLOW
	reloc   90 offset  6d5 [16d5] HIGHLOW
	reloc   91 offset  6de [16de] HIGHLOW
	reloc   92 offset  734 [1734] HIGHLOW
	reloc   93 offset  741 [1741] HIGHLOW
	reloc   94 offset  749 [1749] HIGHLOW
	reloc   95 offset  752 [1752] HIGHLOW
	reloc   96 offset  79d [179d] HIGHLOW
	reloc   97 offset  7a4 [17a4] HIGHLOW
	reloc   98 offset  7aa [17aa] HIGHLOW
	reloc   99 offset  7b5 [17b5] HIGHLOW
	reloc  100 offset  7d9 [17d9] HIGHLOW
	reloc  101 offset  7e8 [17e8] HIGHLOW
	reloc  102 offset  7f1 [17f1] HIGHLOW
	reloc  103 offset  80b [180b] HIGHLOW
	reloc  104 offset  819 [1819] HIGHLOW
	reloc  105 offset  87a [187a] HIGHLOW
	reloc  106 offset  885 [1885] HIGHLOW
	reloc  107 offset  8ae [18ae] HIGHLOW
	reloc  108 offset  8bf [18bf] HIGHLOW
	reloc  109 offset  8c7 [18c7] HIGHLOW
	reloc  110 offset  8ce [18ce] HIGHLOW
	reloc  111 offset  8dd [18dd] HIGHLOW
	reloc  112 offset  8e9 [18e9] HIGHLOW
	reloc  113 offset  8f6 [18f6] HIGHLOW
	reloc  114 offset  8fb [18fb] HIGHLOW
	reloc  115 offset  900 [1900] HIGHLOW
	reloc  116 offset  90c [190c] HIGHLOW
	reloc  117 offset  927 [1927] HIGHLOW
	reloc  118 offset  934 [1934] HIGHLOW
	reloc  119 offset  944 [1944] HIGHLOW
	reloc  120 offset  975 [1975] HIGHLOW
	reloc  121 offset  97b [197b] HIGHLOW
	reloc  122 offset  980 [1980] HIGHLOW
	reloc  123 offset  98c [198c] HIGHLOW
	reloc  124 offset  9a1 [19a1] HIGHLOW
	reloc  125 offset  9ad [19ad] HIGHLOW
	reloc  126 offset  9d5 [19d5] HIGHLOW
	reloc  127 offset  9dc [19dc] HIGHLOW
	reloc  128 offset  9eb [19eb] HIGHLOW
	reloc  129 offset  9f9 [19f9] HIGHLOW
	reloc  130 offset  a01 [1a01] HIGHLOW
	reloc  131 offset  a0b [1a0b] HIGHLOW
	reloc  132 offset  a11 [1a11] HIGHLOW
	reloc  133 offset  a16 [1a16] HIGHLOW
	reloc  134 offset  a22 [1a22] HIGHLOW
	reloc  135 offset  a3a [1a3a] HIGHLOW
	reloc  136 offset  a3f [1a3f] HIGHLOW
	reloc  137 offset  a45 [1a45] HIGHLOW
	reloc  138 offset  a4e [1a4e] HIGHLOW
	reloc  139 offset  a6a [1a6a] HIGHLOW
	reloc  140 offset  a81 [1a81] HIGHLOW
	reloc  141 offset  a9a [1a9a] HIGHLOW
	reloc  142 offset  ab2 [1ab2] HIGHLOW
	reloc  143 offset  ac5 [1ac5] HIGHLOW
	reloc  144 offset  ad3 [1ad3] HIGHLOW
	reloc  145 offset  b0c [1b0c] HIGHLOW
	reloc  146 offset  b10 [1b10] HIGHLOW
	reloc  147 offset  b14 [1b14] HIGHLOW
	reloc  148 offset  b18 [1b18] HIGHLOW
	reloc  149 offset  b1c [1b1c] HIGHLOW
	reloc  150 offset  b20 [1b20] HIGHLOW
	reloc  151 offset  b24 [1b24] HIGHLOW
	reloc  152 offset  b28 [1b28] HIGHLOW
	reloc  153 offset  b2c [1b2c] HIGHLOW
	reloc  154 offset  b30 [1b30] HIGHLOW
	reloc  155 offset  b34 [1b34] HIGHLOW
	reloc  156 offset  b38 [1b38] HIGHLOW
	reloc  157 offset  b3c [1b3c] HIGHLOW
	reloc  158 offset  b53 [1b53] HIGHLOW
	reloc  159 offset  b8b [1b8b] HIGHLOW
	reloc  160 offset  b93 [1b93] HIGHLOW
	reloc  161 offset  b99 [1b99] HIGHLOW
	reloc  162 offset  ba3 [1ba3] HIGHLOW
	reloc  163 offset  ba9 [1ba9] HIGHLOW
	reloc  164 offset  bb1 [1bb1] HIGHLOW
	reloc  165 offset  bba [1bba] HIGHLOW
	reloc  166 offset  bc0 [1bc0] HIGHLOW
	reloc  167 offset  bc5 [1bc5] HIGHLOW
	reloc  168 offset  bd1 [1bd1] HIGHLOW
	reloc  169 offset  be7 [1be7] HIGHLOW
	reloc  170 offset  bfc [1bfc] HIGHLOW
	reloc  171 offset  c03 [1c03] HIGHLOW
	reloc  172 offset  c11 [1c11] HIGHLOW
	reloc  173 offset  c67 [1c67] HIGHLOW
	reloc  174 offset  c7b [1c7b] HIGHLOW
	reloc  175 offset  cbc [1cbc] HIGHLOW
	reloc  176 offset  ce4 [1ce4] HIGHLOW
	reloc  177 offset  d25 [1d25] HIGHLOW
	reloc  178 offset  d4b [1d4b] HIGHLOW
	reloc  179 offset  d72 [1d72] HIGHLOW
	reloc  180 offset  d9d [1d9d] HIGHLOW
	reloc  181 offset  dd1 [1dd1] HIGHLOW
	reloc  182 offset  e0e [1e0e] HIGHLOW
	reloc  183 offset  e3c [1e3c] HIGHLOW
	reloc  184 offset  e45 [1e45] HIGHLOW
	reloc  185 offset  e60 [1e60] HIGHLOW
	reloc  186 offset  e69 [1e69] HIGHLOW
	reloc  187 offset  e84 [1e84] HIGHLOW
	reloc  188 offset  e8d [1e8d] HIGHLOW
	reloc  189 offset  ea8 [1ea8] HIGHLOW
	reloc  190 offset  eb1 [1eb1] HIGHLOW
	reloc  191 offset  ecc [1ecc] HIGHLOW
	reloc  192 offset  ed5 [1ed5] HIGHLOW
	reloc  193 offset  ef0 [1ef0] HIGHLOW
	reloc  194 offset  ef9 [1ef9] HIGHLOW
	reloc  195 offset  f14 [1f14] HIGHLOW
	reloc  196 offset  f1d [1f1d] HIGHLOW
	reloc  197 offset  f38 [1f38] HIGHLOW
	reloc  198 offset  f41 [1f41] HIGHLOW
	reloc  199 offset  f59 [1f59] HIGHLOW
	reloc  200 offset  f62 [1f62] HIGHLOW
	reloc  201 offset  f7a [1f7a] HIGHLOW
	reloc  202 offset  f83 [1f83] HIGHLOW
	reloc  203 offset  f9b [1f9b] HIGHLOW
	reloc  204 offset  fa4 [1fa4] HIGHLOW
	reloc  205 offset  fbd [1fbd] HIGHLOW
	reloc  206 offset  fe4 [1fe4] HIGHLOW
	reloc  207 offset    0 [1000] ABSOLUTE

Virtual Address: 00002000 Chunk size 324 (0x144) Number of fixups 158
	reloc    0 offset   2f [202f] HIGHLOW
	reloc    1 offset   a6 [20a6] HIGHLOW
	reloc    2 offset   f1 [20f1] HIGHLOW
	reloc    3 offset  147 [2147] HIGHLOW
	reloc    4 offset  20b [220b] HIGHLOW
	reloc    5 offset  25f [225f] HIGHLOW
	reloc    6 offset  286 [2286] HIGHLOW
	reloc    7 offset  28e [228e] HIGHLOW
	reloc    8 offset  29a [229a] HIGHLOW
	reloc    9 offset  42c [242c] HIGHLOW
	reloc   10 offset  4b6 [24b6] HIGHLOW
	reloc   11 offset  4c4 [24c4] HIGHLOW
	reloc   12 offset  4dd [24dd] HIGHLOW
	reloc   13 offset  4e1 [24e1] HIGHLOW
	reloc   14 offset  4e5 [24e5] HIGHLOW
	reloc   15 offset  4e9 [24e9] HIGHLOW
	reloc   16 offset  4ed [24ed] HIGHLOW
	reloc   17 offset  4f1 [24f1] HIGHLOW
	reloc   18 offset  4f5 [24f5] HIGHLOW
	reloc   19 offset  517 [2517] HIGHLOW
	reloc   20 offset  52d [252d] HIGHLOW
	reloc   21 offset  534 [2534] HIGHLOW
	reloc   22 offset  54c [254c] HIGHLOW
	reloc   23 offset  57d [257d] HIGHLOW
	reloc   24 offset  595 [2595] HIGHLOW
	reloc   25 offset  5bb [25bb] HIGHLOW
	reloc   26 offset  604 [2604] HIGHLOW
	reloc   27 offset  60f [260f] HIGHLOW
	reloc   28 offset  61c [261c] HIGHLOW
	reloc   29 offset  629 [2629] HIGHLOW
	reloc   30 offset  631 [2631] HIGHLOW
	reloc   31 offset  63b [263b] HIGHLOW
	reloc   32 offset  640 [2640] HIGHLOW
	reloc   33 offset  664 [2664] HIGHLOW
	reloc   34 offset  66f [266f] HIGHLOW
	reloc   35 offset  688 [2688] HIGHLOW
	reloc   36 offset  693 [2693] HIGHLOW
	reloc   37 offset  6ac [26ac] HIGHLOW
	reloc   38 offset  6b7 [26b7] HIGHLOW
	reloc   39 offset  701 [2701] HIGHLOW
	reloc   40 offset  70c [270c] HIGHLOW
	reloc   41 offset  72c [272c] HIGHLOW
	reloc   42 offset  749 [2749] HIGHLOW
	reloc   43 offset  74f [274f] HIGHLOW
	reloc   44 offset  759 [2759] HIGHLOW
	reloc   45 offset  764 [2764] HIGHLOW
	reloc   46 offset  77c [277c] HIGHLOW
	reloc   47 offset  789 [2789] HIGHLOW
	reloc   48 offset  791 [2791] HIGHLOW
	reloc   49 offset  79a [279a] HIGHLOW
	reloc   50 offset  7c1 [27c1] HIGHLOW
	reloc   51 offset  7d8 [27d8] HIGHLOW
	reloc   52 offset  7dd [27dd] HIGHLOW
	reloc   53 offset  7f6 [27f6] HIGHLOW
	reloc   54 offset  815 [2815] HIGHLOW
	reloc   55 offset  838 [2838] HIGHLOW
	reloc   56 offset  84f [284f] HIGHLOW
	reloc   57 offset  862 [2862] HIGHLOW
	reloc   58 offset  867 [2867] HIGHLOW
	reloc   59 offset  880 [2880] HIGHLOW
	reloc   60 offset  890 [2890] HIGHLOW
	reloc   61 offset  8a8 [28a8] HIGHLOW
	reloc   62 offset  8b1 [28b1] HIGHLOW
	reloc   63 offset  8d1 [28d1] HIGHLOW
	reloc   64 offset  8f5 [28f5] HIGHLOW
	reloc   65 offset  900 [2900] HIGHLOW
	reloc   66 offset  959 [2959] HIGHLOW
	reloc   67 offset  961 [2961] HIGHLOW
	reloc   68 offset  96b [296b] HIGHLOW
	reloc   69 offset  978 [2978] HIGHLOW
	reloc   70 offset  981 [2981] HIGHLOW
	reloc   71 offset  99a [299a] HIGHLOW
	reloc   72 offset  9b8 [29b8] HIGHLOW
	reloc   73 offset  9dc [29dc] HIGHLOW
	reloc   74 offset  9e7 [29e7] HIGHLOW
	reloc   75 offset  9f9 [29f9] HIGHLOW
	reloc   76 offset  a0e [2a0e] HIGHLOW
	reloc   77 offset  a15 [2a15] HIGHLOW
	reloc   78 offset  a2a [2a2a] HIGHLOW
	reloc   79 offset  a32 [2a32] HIGHLOW
	reloc   80 offset  a39 [2a39] HIGHLOW
	reloc   81 offset  a3f [2a3f] HIGHLOW
	reloc   82 offset  a4c [2a4c] HIGHLOW
	reloc   83 offset  a55 [2a55] HIGHLOW
	reloc   84 offset  a64 [2a64] HIGHLOW
	reloc   85 offset  a79 [2a79] HIGHLOW
	reloc   86 offset  a98 [2a98] HIGHLOW
	reloc   87 offset  aab [2aab] HIGHLOW
	reloc   88 offset  ab7 [2ab7] HIGHLOW
	reloc   89 offset  ac7 [2ac7] HIGHLOW
	reloc   90 offset  ae6 [2ae6] HIGHLOW
	reloc   91 offset  b08 [2b08] HIGHLOW
	reloc   92 offset  b1c [2b1c] HIGHLOW
	reloc   93 offset  b3c [2b3c] HIGHLOW
	reloc   94 offset  b4b [2b4b] HIGHLOW
	reloc   95 offset  b60 [2b60] HIGHLOW
	reloc   96 offset  b68 [2b68] HIGHLOW
	reloc   97 offset  b7d [2b7d] HIGHLOW
	reloc   98 offset  b85 [2b85] HIGHLOW
	reloc   99 offset  b8c [2b8c] HIGHLOW
	reloc  100 offset  b92 [2b92] HIGHLOW
	reloc  101 offset  b9f [2b9f] HIGHLOW
	reloc  102 offset  ba8 [2ba8] HIGHLOW
	reloc  103 offset  bb5 [2bb5] HIGHLOW
	reloc  104 offset  bc8 [2bc8] HIGHLOW
	reloc  105 offset  bd4 [2bd4] HIGHLOW
	reloc  106 offset  be6 [2be6] HIGHLOW
	reloc  107 offset  bfa [2bfa] HIGHLOW
	reloc  108 offset  c39 [2c39] HIGHLOW
	reloc  109 offset  c3d [2c3d] HIGHLOW
	reloc  110 offset  c41 [2c41] HIGHLOW
	reloc  111 offset  c45 [2c45] HIGHLOW
	reloc  112 offset  c49 [2c49] HIGHLOW
	reloc  113 offset  c4d [2c4d] HIGHLOW
	reloc  114 offset  c51 [2c51] HIGHLOW
	reloc  115 offset  c55 [2c55] HIGHLOW
	reloc  116 offset  c59 [2c59] HIGHLOW
	reloc  117 offset  c5d [2c5d] HIGHLOW
	reloc  118 offset  c61 [2c61] HIGHLOW
	reloc  119 offset  c65 [2c65] HIGHLOW
	reloc  120 offset  c69 [2c69] HIGHLOW
	reloc  121 offset  c90 [2c90] HIGHLOW
	reloc  122 offset  cc6 [2cc6] HIGHLOW
	reloc  123 offset  cee [2cee] HIGHLOW
	reloc  124 offset  d0d [2d0d] HIGHLOW
	reloc  125 offset  d21 [2d21] HIGHLOW
	reloc  126 offset  d2b [2d2b] HIGHLOW
	reloc  127 offset  d3c [2d3c] HIGHLOW
	reloc  128 offset  d4a [2d4a] HIGHLOW
	reloc  129 offset  d5f [2d5f] HIGHLOW
	reloc  130 offset  d6d [2d6d] HIGHLOW
	reloc  131 offset  da7 [2da7] HIGHLOW
	reloc  132 offset  dab [2dab] HIGHLOW
	reloc  133 offset  daf [2daf] HIGHLOW
	reloc  134 offset  db3 [2db3] HIGHLOW
	reloc  135 offset  db7 [2db7] HIGHLOW
	reloc  136 offset  dbb [2dbb] HIGHLOW
	reloc  137 offset  dbf [2dbf] HIGHLOW
	reloc  138 offset  dc3 [2dc3] HIGHLOW
	reloc  139 offset  dc7 [2dc7] HIGHLOW
	reloc  140 offset  dcb [2dcb] HIGHLOW
	reloc  141 offset  dcf [2dcf] HIGHLOW
	reloc  142 offset  dd3 [2dd3] HIGHLOW
	reloc  143 offset  dd7 [2dd7] HIGHLOW
	reloc  144 offset  de7 [2de7] HIGHLOW
	reloc  145 offset  ea9 [2ea9] HIGHLOW
	reloc  146 offset  ec6 [2ec6] HIGHLOW
	reloc  147 offset  ecc [2ecc] HIGHLOW
	reloc  148 offset  ed9 [2ed9] HIGHLOW
	reloc  149 offset  ef4 [2ef4] HIGHLOW
	reloc  150 offset  f00 [2f00] HIGHLOW
	reloc  151 offset  f51 [2f51] HIGHLOW
	reloc  152 offset  f6e [2f6e] HIGHLOW
	reloc  153 offset  fc6 [2fc6] HIGHLOW
	reloc  154 offset  fca [2fca] HIGHLOW
	reloc  155 offset  fce [2fce] HIGHLOW
	reloc  156 offset  fd2 [2fd2] HIGHLOW
	reloc  157 offset  fd6 [2fd6] HIGHLOW

Virtual Address: 00003000 Chunk size 444 (0x1bc) Number of fixups 218
	reloc    0 offset   2f [302f] HIGHLOW
	reloc    1 offset   90 [3090] HIGHLOW
	reloc    2 offset   95 [3095] HIGHLOW
	reloc    3 offset   a1 [30a1] HIGHLOW
	reloc    4 offset   cf [30cf] HIGHLOW
	reloc    5 offset   d3 [30d3] HIGHLOW
	reloc    6 offset   d7 [30d7] HIGHLOW
	reloc    7 offset   db [30db] HIGHLOW
	reloc    8 offset   df [30df] HIGHLOW
	reloc    9 offset   e3 [30e3] HIGHLOW
	reloc   10 offset   e7 [30e7] HIGHLOW
	reloc   11 offset   eb [30eb] HIGHLOW
	reloc   12 offset   ef [30ef] HIGHLOW
	reloc   13 offset   f3 [30f3] HIGHLOW
	reloc   14 offset   f7 [30f7] HIGHLOW
	reloc   15 offset   fb [30fb] HIGHLOW
	reloc   16 offset   ff [30ff] HIGHLOW
	reloc   17 offset  158 [3158] HIGHLOW
	reloc   18 offset  1bd [31bd] HIGHLOW
	reloc   19 offset  1c6 [31c6] HIGHLOW
	reloc   20 offset  1cb [31cb] HIGHLOW
	reloc   21 offset  1d7 [31d7] HIGHLOW
	reloc   22 offset  1f5 [31f5] HIGHLOW
	reloc   23 offset  204 [3204] HIGHLOW
	reloc   24 offset  21a [321a] HIGHLOW
	reloc   25 offset  229 [3229] HIGHLOW
	reloc   26 offset  24c [324c] HIGHLOW
	reloc   27 offset  25b [325b] HIGHLOW
	reloc   28 offset  26e [326e] HIGHLOW
	reloc   29 offset  27d [327d] HIGHLOW
	reloc   30 offset  29d [329d] HIGHLOW
	reloc   31 offset  2ac [32ac] HIGHLOW
	reloc   32 offset  2bf [32bf] HIGHLOW
	reloc   33 offset  2ce [32ce] HIGHLOW
	reloc   34 offset  2d3 [32d3] HIGHLOW
	reloc   35 offset  2df [32df] HIGHLOW
	reloc   36 offset  2f9 [32f9] HIGHLOW
	reloc   37 offset  305 [3305] HIGHLOW
	reloc   38 offset  31c [331c] HIGHLOW
	reloc   39 offset  328 [3328] HIGHLOW
	reloc   40 offset  32d [332d] HIGHLOW
	reloc   41 offset  339 [3339] HIGHLOW
	reloc   42 offset  34d [334d] HIGHLOW
	reloc   43 offset  394 [3394] HIGHLOW
	reloc   44 offset  39f [339f] HIGHLOW
	reloc   45 offset  3a9 [33a9] HIGHLOW
	reloc   46 offset  3b4 [33b4] HIGHLOW
	reloc   47 offset  3e3 [33e3] HIGHLOW
	reloc   48 offset  416 [3416] HIGHLOW
	reloc   49 offset  451 [3451] HIGHLOW
	reloc   50 offset  473 [3473] HIGHLOW
	reloc   51 offset  47e [347e] HIGHLOW
	reloc   52 offset  4a7 [34a7] HIGHLOW
	reloc   53 offset  4c3 [34c3] HIGHLOW
	reloc   54 offset  4ce [34ce] HIGHLOW
	reloc   55 offset  505 [3505] HIGHLOW
	reloc   56 offset  52c [352c] HIGHLOW
	reloc   57 offset  531 [3531] HIGHLOW
	reloc   58 offset  549 [3549] HIGHLOW
	reloc   59 offset  556 [3556] HIGHLOW
	reloc   60 offset  565 [3565] HIGHLOW
	reloc   61 offset  580 [3580] HIGHLOW
	reloc   62 offset  59a [359a] HIGHLOW
	reloc   63 offset  5a6 [35a6] HIGHLOW
	reloc   64 offset  5dc [35dc] HIGHLOW
	reloc   65 offset  5e5 [35e5] HIGHLOW
	reloc   66 offset  5fc [35fc] HIGHLOW
	reloc   67 offset  62a [362a] HIGHLOW
	reloc   68 offset  632 [3632] HIGHLOW
	reloc   69 offset  638 [3638] HIGHLOW
	reloc   70 offset  641 [3641] HIGHLOW
	reloc   71 offset  652 [3652] HIGHLOW
	reloc   72 offset  65a [365a] HIGHLOW
	reloc   73 offset  68c [368c] HIGHLOW
	reloc   74 offset  694 [3694] HIGHLOW
	reloc   75 offset  69a [369a] HIGHLOW
	reloc   76 offset  6b0 [36b0] HIGHLOW
	reloc   77 offset  6b6 [36b6] HIGHLOW
	reloc   78 offset  6e0 [36e0] HIGHLOW
	reloc   79 offset  6f4 [36f4] HIGHLOW
	reloc   80 offset  704 [3704] HIGHLOW
	reloc   81 offset  70c [370c] HIGHLOW
	reloc   82 offset  715 [3715] HIGHLOW
	reloc   83 offset  723 [3723] HIGHLOW
	reloc   84 offset  742 [3742] HIGHLOW
	reloc   85 offset  74e [374e] HIGHLOW
	reloc   86 offset  75a [375a] HIGHLOW
	reloc   87 offset  766 [3766] HIGHLOW
	reloc   88 offset  771 [3771] HIGHLOW
	reloc   89 offset  77d [377d] HIGHLOW
	reloc   90 offset  789 [3789] HIGHLOW
	reloc   91 offset  795 [3795] HIGHLOW
	reloc   92 offset  7a4 [37a4] HIGHLOW
	reloc   93 offset  7af [37af] HIGHLOW
	reloc   94 offset  7b7 [37b7] HIGHLOW
	reloc   95 offset  7c5 [37c5] HIGHLOW
	reloc   96 offset  7cb [37cb] HIGHLOW
	reloc   97 offset  7d4 [37d4] HIGHLOW
	reloc   98 offset  7dc [37dc] HIGHLOW
	reloc   99 offset  7e6 [37e6] HIGHLOW
	reloc  100 offset  7eb [37eb] HIGHLOW
	reloc  101 offset  7f9 [37f9] HIGHLOW
	reloc  102 offset  801 [3801] HIGHLOW
	reloc  103 offset  80a [380a] HIGHLOW
	reloc  104 offset  81b [381b] HIGHLOW
	reloc  105 offset  827 [3827] HIGHLOW
	reloc  106 offset  837 [3837] HIGHLOW
	reloc  107 offset  844 [3844] HIGHLOW
	reloc  108 offset  84c [384c] HIGHLOW
	reloc  109 offset  855 [3855] HIGHLOW
	reloc  110 offset  866 [3866] HIGHLOW
	reloc  111 offset  870 [3870] HIGHLOW
	reloc  112 offset  87f [387f] HIGHLOW
	reloc  113 offset  893 [3893] HIGHLOW
	reloc  114 offset  8a4 [38a4] HIGHLOW
	reloc  115 offset  8ad [38ad] HIGHLOW
	reloc  116 offset  8b5 [38b5] HIGHLOW
	reloc  117 offset  8be [38be] HIGHLOW
	reloc  118 offset  8cf [38cf] HIGHLOW
	reloc  119 offset  8da [38da] HIGHLOW
	reloc  120 offset  95a [395a] HIGHLOW
	reloc  121 offset  967 [3967] HIGHLOW
	reloc  122 offset  99f [399f] HIGHLOW
	reloc  123 offset  9f0 [39f0] HIGHLOW
	reloc  124 offset  a3c [3a3c] HIGHLOW
	reloc  125 offset  a4b [3a4b] HIGHLOW
	reloc  126 offset  a53 [3a53] HIGHLOW
	reloc  127 offset  a6a [3a6a] HIGHLOW
	reloc  128 offset  a9a [3a9a] HIGHLOW
	reloc  129 offset  aa1 [3aa1] HIGHLOW
	reloc  130 offset  aaa [3aaa] HIGHLOW
	reloc  131 offset  ab1 [3ab1] HIGHLOW
	reloc  132 offset  ad5 [3ad5] HIGHLOW
	reloc  133 offset  adc [3adc] HIGHLOW
	reloc  134 offset  aed [3aed] HIGHLOW
	reloc  135 offset  af4 [3af4] HIGHLOW
	reloc  136 offset  afb [3afb] HIGHLOW
	reloc  137 offset  b02 [3b02] HIGHLOW
	reloc  138 offset  b15 [3b15] HIGHLOW
	reloc  139 offset  b1c [3b1c] HIGHLOW
	reloc  140 offset  b2d [3b2d] HIGHLOW
	reloc  141 offset  b34 [3b34] HIGHLOW
	reloc  142 offset  b5c [3b5c] HIGHLOW
	reloc  143 offset  b60 [3b60] HIGHLOW
	reloc  144 offset  b64 [3b64] HIGHLOW
	reloc  145 offset  b68 [3b68] HIGHLOW
	reloc  146 offset  b6c [3b6c] HIGHLOW
	reloc  147 offset  b70 [3b70] HIGHLOW
	reloc  148 offset  b74 [3b74] HIGHLOW
	reloc  149 offset  b78 [3b78] HIGHLOW
	reloc  150 offset  b7c [3b7c] HIGHLOW
	reloc  151 offset  b80 [3b80] HIGHLOW
	reloc  152 offset  b84 [3b84] HIGHLOW
	reloc  153 offset  b88 [3b88] HIGHLOW
	reloc  154 offset  b8c [3b8c] HIGHLOW
	reloc  155 offset  b94 [3b94] HIGHLOW
	reloc  156 offset  b9b [3b9b] HIGHLOW
	reloc  157 offset  bb8 [3bb8] HIGHLOW
	reloc  158 offset  bc7 [3bc7] HIGHLOW
	reloc  159 offset  bdb [3bdb] HIGHLOW
	reloc  160 offset  be2 [3be2] HIGHLOW
	reloc  161 offset  bf4 [3bf4] HIGHLOW
	reloc  162 offset  bfa [3bfa] HIGHLOW
	reloc  163 offset  c06 [3c06] HIGHLOW
	reloc  164 offset  c0d [3c0d] HIGHLOW
	reloc  165 offset  c28 [3c28] HIGHLOW
	reloc  166 offset  c37 [3c37] HIGHLOW
	reloc  167 offset  c75 [3c75] HIGHLOW
	reloc  168 offset  c83 [3c83] HIGHLOW
	reloc  169 offset  cbe [3cbe] HIGHLOW
	reloc  170 offset  cca [3cca] HIGHLOW
	reloc  171 offset  cd3 [3cd3] HIGHLOW
	reloc  172 offset  cdb [3cdb] HIGHLOW
	reloc  173 offset  ce1 [3ce1] HIGHLOW
	reloc  174 offset  ce6 [3ce6] HIGHLOW
	reloc  175 offset  cf2 [3cf2] HIGHLOW
	reloc  176 offset  cfb [3cfb] HIGHLOW
	reloc  177 offset  d0a [3d0a] HIGHLOW
	reloc  178 offset  d15 [3d15] HIGHLOW
	reloc  179 offset  d4a [3d4a] HIGHLOW
	reloc  180 offset  d56 [3d56] HIGHLOW
	reloc  181 offset  d5f [3d5f] HIGHLOW
	reloc  182 offset  d67 [3d67] HIGHLOW
	reloc  183 offset  d6d [3d6d] HIGHLOW
	reloc  184 offset  d73 [3d73] HIGHLOW
	reloc  185 offset  d79 [3d79] HIGHLOW
	reloc  186 offset  d7e [3d7e] HIGHLOW
	reloc  187 offset  d8a [3d8a] HIGHLOW
	reloc  188 offset  d97 [3d97] HIGHLOW
	reloc  189 offset  da4 [3da4] HIGHLOW
	reloc  190 offset  db0 [3db0] HIGHLOW
	reloc  191 offset  dc2 [3dc2] HIGHLOW
	reloc  192 offset  dc8 [3dc8] HIGHLOW
	reloc  193 offset  de0 [3de0] HIGHLOW
	reloc  194 offset  de6 [3de6] HIGHLOW
	reloc  195 offset  df3 [3df3] HIGHLOW
	reloc  196 offset  e0b [3e0b] HIGHLOW
	reloc  197 offset  e17 [3e17] HIGHLOW
	reloc  198 offset  e1f [3e1f] HIGHLOW
	reloc  199 offset  e28 [3e28] HIGHLOW
	reloc  200 offset  e35 [3e35] HIGHLOW
	reloc  201 offset  e46 [3e46] HIGHLOW
	reloc  202 offset  e65 [3e65] HIGHLOW
	reloc  203 offset  e6d [3e6d] HIGHLOW
	reloc  204 offset  e84 [3e84] HIGHLOW
	reloc  205 offset  e8b [3e8b] HIGHLOW
	reloc  206 offset  e9e [3e9e] HIGHLOW
	reloc  207 offset  ea4 [3ea4] HIGHLOW
	reloc  208 offset  eaa [3eaa] HIGHLOW
	reloc  209 offset  eb0 [3eb0] HIGHLOW
	reloc  210 offset  eb6 [3eb6] HIGHLOW
	reloc  211 offset  edb [3edb] HIGHLOW
	reloc  212 offset  ef3 [3ef3] HIGHLOW
	reloc  213 offset  efc [3efc] HIGHLOW
	reloc  214 offset  f1f [3f1f] HIGHLOW
	reloc  215 offset  f33 [3f33] HIGHLOW
	reloc  216 offset  f40 [3f40] HIGHLOW
	reloc  217 offset    0 [3000] ABSOLUTE

Virtual Address: 00005000 Chunk size 92 (0x5c) Number of fixups 42
	reloc    0 offset    0 [5000] HIGHLOW
	reloc    1 offset    8 [5008] HIGHLOW
	reloc    2 offset   10 [5010] HIGHLOW
	reloc    3 offset   18 [5018] HIGHLOW
	reloc    4 offset   20 [5020] HIGHLOW
	reloc    5 offset   28 [5028] HIGHLOW
	reloc    6 offset   30 [5030] HIGHLOW
	reloc    7 offset   38 [5038] HIGHLOW
	reloc    8 offset   40 [5040] HIGHLOW
	reloc    9 offset   48 [5048] HIGHLOW
	reloc   10 offset   50 [5050] HIGHLOW
	reloc   11 offset   58 [5058] HIGHLOW
	reloc   12 offset   60 [5060] HIGHLOW
	reloc   13 offset   68 [5068] HIGHLOW
	reloc   14 offset   70 [5070] HIGHLOW
	reloc   15 offset   78 [5078] HIGHLOW
	reloc   16 offset   80 [5080] HIGHLOW
	reloc   17 offset   88 [5088] HIGHLOW
	reloc   18 offset   90 [5090] HIGHLOW
	reloc   19 offset   98 [5098] HIGHLOW
	reloc   20 offset   a0 [50a0] HIGHLOW
	reloc   21 offset   a8 [50a8] HIGHLOW
	reloc   22 offset   b0 [50b0] HIGHLOW
	reloc   23 offset   b8 [50b8] HIGHLOW
	reloc   24 offset   c0 [50c0] HIGHLOW
	reloc   25 offset   c8 [50c8] HIGHLOW
	reloc   26 offset   d0 [50d0] HIGHLOW
	reloc   27 offset   d8 [50d8] HIGHLOW
	reloc   28 offset   e0 [50e0] HIGHLOW
	reloc   29 offset   e8 [50e8] HIGHLOW
	reloc   30 offset   f0 [50f0] HIGHLOW
	reloc   31 offset   f8 [50f8] HIGHLOW
	reloc   32 offset  100 [5100] HIGHLOW
	reloc   33 offset  108 [5108] HIGHLOW
	reloc   34 offset  110 [5110] HIGHLOW
	reloc   35 offset  118 [5118] HIGHLOW
	reloc   36 offset  120 [5120] HIGHLOW
	reloc   37 offset  128 [5128] HIGHLOW
	reloc   38 offset  130 [5130] HIGHLOW
	reloc   39 offset  138 [5138] HIGHLOW
	reloc   40 offset  140 [5140] HIGHLOW
	reloc   41 offset  148 [5148] HIGHLOW

Virtual Address: 00006000 Chunk size 164 (0xa4) Number of fixups 78
	reloc    0 offset   3c [603c] HIGHLOW
	reloc    1 offset  220 [6220] HIGHLOW
	reloc    2 offset  400 [6400] HIGHLOW
	reloc    3 offset  550 [6550] HIGHLOW
	reloc    4 offset  79c [679c] HIGHLOW
	reloc    5 offset  7a0 [67a0] HIGHLOW
	reloc    6 offset  7a4 [67a4] HIGHLOW
	reloc    7 offset  7a8 [67a8] HIGHLOW
	reloc    8 offset  7ac [67ac] HIGHLOW
	reloc    9 offset  7b0 [67b0] HIGHLOW
	reloc   10 offset  7b4 [67b4] HIGHLOW
	reloc   11 offset  7b8 [67b8] HIGHLOW
	reloc   12 offset  7bc [67bc] HIGHLOW
	reloc   13 offset  7c0 [67c0] HIGHLOW
	reloc   14 offset  8a0 [68a0] HIGHLOW
	reloc   15 offset  8a8 [68a8] HIGHLOW
	reloc   16 offset  8b0 [68b0] HIGHLOW
	reloc   17 offset  8b8 [68b8] HIGHLOW
	reloc   18 offset  8c0 [68c0] HIGHLOW
	reloc   19 offset  8c8 [68c8] HIGHLOW
	reloc   20 offset  8d0 [68d0] HIGHLOW
	reloc   21 offset  8d8 [68d8] HIGHLOW
	reloc   22 offset  8e0 [68e0] HIGHLOW
	reloc   23 offset  8e8 [68e8] HIGHLOW
	reloc   24 offset  8f0 [68f0] HIGHLOW
	reloc   25 offset  8f8 [68f8] HIGHLOW
	reloc   26 offset  900 [6900] HIGHLOW
	reloc   27 offset  908 [6908] HIGHLOW
	reloc   28 offset  910 [6910] HIGHLOW
	reloc   29 offset  918 [6918] HIGHLOW
	reloc   30 offset  920 [6920] HIGHLOW
	reloc   31 offset  928 [6928] HIGHLOW
	reloc   32 offset  930 [6930] HIGHLOW
	reloc   33 offset  938 [6938] HIGHLOW
	reloc   34 offset  940 [6940] HIGHLOW
	reloc   35 offset  948 [6948] HIGHLOW
	reloc   36 offset  950 [6950] HIGHLOW
	reloc   37 offset  958 [6958] HIGHLOW
	reloc   38 offset  960 [6960] HIGHLOW
	reloc   39 offset  968 [6968] HIGHLOW
	reloc   40 offset  970 [6970] HIGHLOW
	reloc   41 offset  978 [6978] HIGHLOW
	reloc   42 offset  980 [6980] HIGHLOW
	reloc   43 offset  988 [6988] HIGHLOW
	reloc   44 offset  990 [6990] HIGHLOW
	reloc   45 offset  9e0 [69e0] HIGHLOW
	reloc   46 offset  ab8 [6ab8] HIGHLOW
	reloc   47 offset  ac0 [6ac0] HIGHLOW
	reloc   48 offset  ac4 [6ac4] HIGHLOW
	reloc   49 offset  ad0 [6ad0] HIGHLOW
	reloc   50 offset  ad8 [6ad8] HIGHLOW
	reloc   51 offset  adc [6adc] HIGHLOW
	reloc   52 offset  ae8 [6ae8] HIGHLOW
	reloc   53 offset  af0 [6af0] HIGHLOW
	reloc   54 offset  af4 [6af4] HIGHLOW
	reloc   55 offset  b00 [6b00] HIGHLOW
	reloc   56 offset  b08 [6b08] HIGHLOW
	reloc   57 offset  b0c [6b0c] HIGHLOW
	reloc   58 offset  b18 [6b18] HIGHLOW
	reloc   59 offset  b20 [6b20] HIGHLOW
	reloc   60 offset  b24 [6b24] HIGHLOW
	reloc   61 offset  c0c [6c0c] HIGHLOW
	reloc   62 offset  c60 [6c60] HIGHLOW
	reloc   63 offset  c64 [6c64] HIGHLOW
	reloc   64 offset  c68 [6c68] HIGHLOW
	reloc   65 offset  c6c [6c6c] HIGHLOW
	reloc   66 offset  c70 [6c70] HIGHLOW
	reloc   67 offset  c74 [6c74] HIGHLOW
	reloc   68 offset  c78 [6c78] HIGHLOW
	reloc   69 offset  c7c [6c7c] HIGHLOW
	reloc   70 offset  c80 [6c80] HIGHLOW
	reloc   71 offset  c84 [6c84] HIGHLOW
	reloc   72 offset  c88 [6c88] HIGHLOW
	reloc   73 offset  c8c [6c8c] HIGHLOW
	reloc   74 offset  c90 [6c90] HIGHLOW
	reloc   75 offset  d30 [6d30] HIGHLOW
	reloc   76 offset  d34 [6d34] HIGHLOW
	reloc   77 offset  d58 [6d58] HIGHLOW

Sections:
Idx Name          Size      VMA               LMA               File off  Algn
  0 .text         00002f50  80001000  80001000  00000400  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, CODE, LINK_ONCE_DISCARD
  1 .bss          00000034  80004000  80004000  00000000  2**2
                  ALLOC
  2 .exc          00000154  80005000  80005000  00003400  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA, LINK_ONCE_DISCARD
  3 .data         00000d60  80006000  80006000  00003600  2**2
                  CONTENTS, ALLOC, LOAD, DATA
  4 .idata        0000058f  80007000  80007000  00004400  2**2
                  CONTENTS, ALLOC, LOAD, DATA, LINK_ONCE_DISCARD
  5 .edata        0000005f  80008000  80008000  00004a00  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  6 .reloc        000005a8  80009000  80009000  00004c00  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
SYMBOL TABLE:
no symbols

```