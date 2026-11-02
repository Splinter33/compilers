```text
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ touch vector_math.h
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ touch vector_math.c
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ touch main.cpp
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ gcc -c vector_math.c -o vector_math.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ ar rcs libmath_static.a vector_math.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ -c main.cpp -o main.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ main.o -L. -lmath_static -o app_static
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ ./app_static
Library version: v2.4.1-release
Dot product result: 32
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ nm main.o
                 U _GLOBAL_OFFSET_TABLE_
                 U _ZNSolsEPFRSoS_E
                 U _ZNSolsEi
0000000000000027 r _ZNSt8__detail30__integer_to_chars_is_unsignedIjEE
0000000000000028 r _ZNSt8__detail30__integer_to_chars_is_unsignedImEE
0000000000000029 r _ZNSt8__detail30__integer_to_chars_is_unsignedIyEE
                 U _ZSt21ios_base_library_initv
                 U _ZSt4cout
                 U _ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_
                 U _ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
                 U __stack_chk_fail
                 U dot_product
                 U get_lib_version
0000000000000000 T main
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ gcc -c vector_math.c -o vector_math_nopic.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ gcc -shared -o libmath_broken.so vector_math_nopic.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ gcc -c -fPIC vector_math.c -o vector_math_pic.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ gcc -shared -o libmath_dynamic.so vector_math_pic.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ main.o -L. -lmath_dynamic -o app_dynamic
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ LD_LIBRARY_PATH=. ./app_dynamic
Library version: v2.4.1-release
Dot product result: 32
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ size app_static app_dynamic
   text    data     bss     dec     hex filename
   2548     656     280    3484     d9c app_static
   2517     680     280    3477     d95 app_dynamic
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ -L. -lmath_dynamic main.o -o app_wrong_order
/usr/bin/ld: main.o: in function `main':
main.cpp:(.text+0x63): undefined reference to `get_lib_version'
/usr/bin/ld: main.cpp:(.text+0xb4): undefined reference to `dot_product'
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ main.o -L. -lmath_dynamic -o app_correct
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ -Wl,--as-needed -L. -lmath_dynamic main.o -o app_wrong_order
/usr/bin/ld: main.o: in function `main':
main.cpp:(.text+0x63): undefined reference to `get_lib_version'
/usr/bin/ld: main.cpp:(.text+0xb4): undefined reference to `dot_product'
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ -c main.cpp -o main.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ main.o -L. -lmath_dynamic -o app_no_extern
/usr/bin/ld: main.o: in function `main':
main.cpp:(.text+0x63): undefined reference to `get_lib_version()'
/usr/bin/ld: main.cpp:(.text+0xb4): undefined reference to `dot_product(int const*, int const*, int)'
collect2: error: ld returned 1 exit status
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ nm main.o | grep -E 'dot|get_lib'
                 U _Z11dot_productPKiS0_i
                 U _Z15get_lib_versionv
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ nm libmath_dynamic.so | grep -E 'dot|get_lib'
000000000000110a T dot_product
00000000000010f9 T get_lib_version
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ -c main.cpp -o main.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ g++ main.o -L. -lmath_dynamic -o app_correct
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab3$ LD_LIBRARY_PATH=. ./app_correct
Library version: v2.4.1-release
Dot product result: 32
```