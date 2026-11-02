```text
piros@DESKTOP-HVQ9RGF:~/lab1$ cd /mnt/c/Users/piros/Desktop/COMILATORS/lab1
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ ls
 legacy.c  'Платформы и среды ЯП задание 001.md'
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ touch simple.cpp
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ g++ -E simple.cpp -o simple.i
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ wc -l simple.cpp simple.i
   22 simple.cpp
 1073 simple.i
 1095 total
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ g++ -S -masm=intel -O0 simple.cpp -o simple_O0.s
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ g++ -S -masm=intel -O2 simple.cpp -o simple_O2.s
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ wc -c simple_O0.s simple_02.s
2497 simple_O0.s
wc: simple_02.s: No such file or directory
2497 total
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ wc -c simple_O0.s simple_O2.s
2497 simple_O0.s
1692 simple_O2.s
4189 total
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ g++ -c simple.cpp -o simple.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ nm -C simple.o
0000000000000044 T bump_counter()
0000000000000013 T sum_of_squares(int, int)
0000000000000000 T square(int)
0000000000000000 r MAGIC
0000000000000000 B global_counter
000000000000005e T main
                 U printf
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ size simple.o
   text    data     bss     dec     hex filename
    400       0       4     404     194 simple.o
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ g++ simple.o -o simple
piros@DESKTOP-HVQ9RGF:/mnt/c/Users/piros/Desktop/COMILATORS/lab1$ ./simple
Result: 25, Counter: 1, Magic: 42
```
