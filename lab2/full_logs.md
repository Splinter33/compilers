```text
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ size core.o legacy.o hotfix.o main.o
   text    data     bss     dec     hex filename
    266    4040   50000   54306    d422 core.o
    172       0       4     176      b0 legacy.o
    127       0       0     127      7f hotfix.o
    118       0       0     118      76 main.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ ls -l *.o
-rwxrwxrwx 1 piros piros 6200 Oct  5 10:54 core.o
-rwxrwxrwx 1 piros piros 1456 Oct  5 10:54 hotfix.o
-rwxrwxrwx 1 piros piros 1608 Oct  5 10:54 legacy.o
-rwxrwxrwx 1 piros piros 1448 Oct  5 10:54 main.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ readelf -SW core.o
There are 16 section headers, starting at offset 0x1438:

Section Headers:
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .text             PROGBITS        0000000000000000 000040 000046 00  AX  0   0  1
  [ 2] .rela.text        RELA            0000000000000000 0012e8 000078 18   I 13   1  8
  [ 3] .data             PROGBITS        0000000000000000 000088 000fc0 00  WA  0   0 32
  [ 4] .bss              NOBITS          0000000000000000 001048 00c350 00  WA  0   0 32
  [ 5] .rodata           PROGBITS        0000000000000000 001048 00004c 00   A  0   0 16
  [ 6] .data.rel.local   PROGBITS        0000000000000000 001098 000008 00  WA  0   0  8
  [ 7] .rela.data.rel.local RELA            0000000000000000 001360 000018 18   I 13   6  8
  [ 8] .comment          PROGBITS        0000000000000000 0010a0 000027 01  MS  0   0  1
  [ 9] .note.GNU-stack   PROGBITS        0000000000000000 0010c7 000000 00      0   0  1
  [10] .note.gnu.property NOTE            0000000000000000 0010c8 000020 00   A  0   0  8
  [11] .eh_frame         PROGBITS        0000000000000000 0010e8 000058 00   A  0   0  8
  [12] .rela.eh_frame    RELA            0000000000000000 001378 000030 18   I 13  11  8
  [13] .symtab           SYMTAB          0000000000000000 001140 000138 18     14   7  8
  [14] .strtab           STRTAB          0000000000000000 001278 00006c 00      0   0  1
  [15] .shstrtab         STRTAB          0000000000000000 0013a8 000089 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  D (mbind), l (large), p (processor specific)
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ readelf -SW legacy.o
There are 13 section headers, starting at offset 0x308:

Section Headers:
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .text             PROGBITS        0000000000000000 000040 000034 00  AX  0   0  1
  [ 2] .rela.text        RELA            0000000000000000 000220 000048 18   I 10   1  8
  [ 3] .data             PROGBITS        0000000000000000 000074 000000 00  WA  0   0  1
  [ 4] .bss              NOBITS          0000000000000000 000074 000004 00  WA  0   0  4
  [ 5] .comment          PROGBITS        0000000000000000 000074 000027 01  MS  0   0  1
  [ 6] .note.GNU-stack   PROGBITS        0000000000000000 00009b 000000 00      0   0  1
  [ 7] .note.gnu.property NOTE            0000000000000000 0000a0 000020 00   A  0   0  8
  [ 8] .eh_frame         PROGBITS        0000000000000000 0000c0 000058 00   A  0   0  8
  [ 9] .rela.eh_frame    RELA            0000000000000000 000268 000030 18   I 10   8  8
  [10] .symtab           SYMTAB          0000000000000000 000118 0000c0 18     11   6  8
  [11] .strtab           STRTAB          0000000000000000 0001d8 000046 00      0   0  1
  [12] .shstrtab         STRTAB          0000000000000000 000298 00006c 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  D (mbind), l (large), p (processor specific)
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ readelf -SW hotfix.o
There are 13 section headers, starting at offset 0x270:

Section Headers:
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .text             PROGBITS        0000000000000000 000040 000027 00  AX  0   0  1
  [ 2] .rela.text        RELA            0000000000000000 000188 000060 18   I 10   1  8
  [ 3] .data             PROGBITS        0000000000000000 000067 000000 00  WA  0   0  1
  [ 4] .bss              NOBITS          0000000000000000 000067 000000 00  WA  0   0  1
  [ 5] .comment          PROGBITS        0000000000000000 000067 000027 01  MS  0   0  1
  [ 6] .note.GNU-stack   PROGBITS        0000000000000000 00008e 000000 00      0   0  1
  [ 7] .note.gnu.property NOTE            0000000000000000 000090 000020 00   A  0   0  8
  [ 8] .eh_frame         PROGBITS        0000000000000000 0000b0 000038 00   A  0   0  8
  [ 9] .rela.eh_frame    RELA            0000000000000000 0001e8 000018 18   I 10   8  8
  [10] .symtab           SYMTAB          0000000000000000 0000e8 000078 18     11   3  8
  [11] .strtab           STRTAB          0000000000000000 000160 000023 00      0   0  1
  [12] .shstrtab         STRTAB          0000000000000000 000200 00006c 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  D (mbind), l (large), p (processor specific)
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ strings -a core.o
System Initialized v1.0
FLAG{b1nary_4rch4eology_2026}
%s, Mode: %d
GCC: (Ubuntu 15.2.0-16ubuntu1) 15.2.0
core.c
large_buffer
internal_cleanup
system_mode
config_table
welcome_msg
secret_token
print_status
printf
.symtab
.strtab
.shstrtab
.rela.text
.data
.bss
.rodata
.rela.data.rel.local
.comment
.note.GNU-stack
.note.gnu.property
.rela.eh_frame
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ nm -A core.o legacy.o hotfix.o main.o
core.o:0000000000000020 D config_table
core.o:0000000000000000 t internal_cleanup
core.o:0000000000000000 b large_buffer
core.o:0000000000000012 T print_status
core.o:                 U printf
core.o:0000000000000020 R secret_token
core.o:0000000000000000 D system_mode
core.o:0000000000000000 D welcome_msg
legacy.o:000000000000001a T apply_legacy_patch
legacy.o:0000000000000000 b legacy_counter
legacy.o:0000000000000000 t legacy_helper
legacy.o:0000000000000004 C system_mode
hotfix.o:0000000000000000 T apply_hotfix
hotfix.o:0000000000000004 C system_mode
main.o:                 U apply_hotfix
main.o:0000000000000000 T main
main.o:                 U print_status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ readelf -sW core.o legacy.o hotfix.o main.o

File: core.o

Symbol table '.symtab' contains 13 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS core.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 .text
     3: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 .bss
     4: 0000000000000000 50000 OBJECT  LOCAL  DEFAULT    4 large_buffer
     5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 .rodata
     6: 0000000000000000    18 FUNC    LOCAL  DEFAULT    1 internal_cleanup
     7: 0000000000000000     4 OBJECT  GLOBAL DEFAULT    3 system_mode
     8: 0000000000000020  4000 OBJECT  GLOBAL DEFAULT    3 config_table
     9: 0000000000000000     8 OBJECT  GLOBAL DEFAULT    6 welcome_msg
    10: 0000000000000020    30 OBJECT  GLOBAL DEFAULT    5 secret_token
    11: 0000000000000012    52 FUNC    GLOBAL DEFAULT    1 print_status
    12: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND printf

File: legacy.o

Symbol table '.symtab' contains 8 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS legacy.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 .text
     3: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 .bss
     4: 0000000000000000     4 OBJECT  LOCAL  DEFAULT    4 legacy_counter
     5: 0000000000000000    26 FUNC    LOCAL  DEFAULT    1 legacy_helper
     6: 0000000000000004     4 OBJECT  GLOBAL DEFAULT  COM system_mode
     7: 000000000000001a    26 FUNC    GLOBAL DEFAULT    1 apply_legacy_patch

File: hotfix.o

Symbol table '.symtab' contains 5 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS hotfix.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 .text
     3: 0000000000000001     4 OBJECT  GLOBAL DEFAULT  COM system_mode
     4: 0000000000000000    39 FUNC    GLOBAL DEFAULT    1 apply_hotfix

File: main.o

Symbol table '.symtab' contains 6 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS main.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 .text
     3: 0000000000000000    30 FUNC    GLOBAL DEFAULT    1 main
     4: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND print_status
     5: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND apply_hotfix
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fcommon core.o legacy.o hotfix.o main.o -o app
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ nm -S app | grep system_mode
0000000000004020 0000000000000004 D system_mode
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ readelf -sW app | grep system_mode
    33: 0000000000004020     4 OBJECT  GLOBAL DEFAULT   25 system_mode
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fno-common main.o hotfix.o legacy.o core.o -o app_better
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fno-common -c hotfix.c -o hotfix_nocommon.o
cc1: fatal error: hotfix.c: No such file or directory
compilation terminated.
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc main.o hotfix_nocommon.o legacy.o core.o -o app_better
/usr/bin/ld: cannot find hotfix_nocommon.o: No such file or directory
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ touch hotfix.c
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fno-common -c hotfix.c -o hotfix_nocommon.o
hotfix.c: In function ‘apply_hotfix’:
hotfix.c:4:1: error: stray ‘\302’ in program
    4 | <U+00A0> system_mode[0] = 'A';
      | ^~~~~~~~
hotfix.c:5:1: error: stray ‘\302’ in program
    5 | <U+00A0> system_mode[1] = 'B';
      | ^~~~~~~~
hotfix.c:6:1: error: stray ‘\302’ in program
    6 | <U+00A0> system_mode[2] = 'C';
      | ^~~~~~~~
hotfix.c:7:1: error: stray ‘\302’ in program
    7 | <U+00A0> system_mode[3] = '\0';
      | ^~~~~~~~
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc main.o hotfix_nocommon.o legacy.o core.o -o app_better
/usr/bin/ld: cannot find hotfix_nocommon.o: No such file or directory
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ sed -i 's/\xC2\xA0/ /g' hotfix.c
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fno-common -c hotfix.c -o hotfix_nocommon.o &&
gcc main.o hotfix_nocommon.o legacy.o core.o -o app_better
/usr/bin/ld: warning: alignment 1 of normal symbol `system_mode' in hotfix_nocommon.o is smaller than 4 used by the common definition in legacy.o
/usr/bin/ld: warning: NOTE: alignment discrepancies can cause real problems.  Investigation is advised.
/usr/bin/ld: core.o:(.data+0x0): multiple definition of `system_mode'; hotfix_nocommon.o:(.bss+0x0): first defined here
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ sed -i 's/^char system_mode/static char system_mode/' hotfix.c
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$ gcc -fno-common -c hotfix.c -o hotfix_nocommon.o &&
> gcc main.o hotfix_nocommon.o legacy.o core.o -o app_better
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab2$
```