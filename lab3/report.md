# Лабораторная работа 3

## 1. Статическая библиотека

```bash
gcc -c vector_math.c -o vector_math.o
ar rcs libmath_static.a vector_math.o
g++ -c main.cpp -o main.o
g++ main.o -L. -lmath_static -o app_static
./app_static
```

Вывод:

```text
Library version: v2.4.1-release
Dot product result: 32
```

Флаги `ar`: `r` - добавление или замена файлов в архиве, `c` - создание архива без предупреждения, `s` - создание индекса символов. Повторный запуск заменит одноименный объектный файл в архиве.

Команда `nm main.o`, значимые строки:

```text
                 U dot_product
                 U get_lib_version
0000000000000000 T main
```

`U` обозначает неопределенный символ, `T` - символ в секции кода. В используемой реализации C++ функция `main` имеет специальное имя без name mangling, необходимое коду запуска программы.

## 2. Динамическая библиотека

```bash
gcc -c vector_math.c -o vector_math_nopic.o
gcc -shared -o libmath_broken.so vector_math_nopic.o
```

Обе команды завершились без сообщений. В данном окружении библиотека из этого исходного кода собралась без `-fPIC`. Ожидаемая в задании ошибка не возникла.

Сборка с PIC:

```bash
gcc -c -fPIC vector_math.c -o vector_math_pic.o
gcc -shared -o libmath_dynamic.so vector_math_pic.o
g++ main.o -L. -lmath_dynamic -o app_dynamic
LD_LIBRARY_PATH=. ./app_dynamic
```

Вывод:

```text
Library version: v2.4.1-release
Dot product result: 32
```

Команда `size app_static app_dynamic`:

```text
   text    data     bss     dec     hex filename
   2548     656     280    3484     d9c app_static
   2517     680     280    3477     d95 app_dynamic
```

Размер `text` уменьшился на 31 байт. В динамическом варианте код функций находится в `libmath_dynamic.so`, которая загружается при запуске. Разница размеров учитывает также служебный код динамического связывания.

## 3. Порядок компоновки

```bash
g++ -L. -lmath_dynamic main.o -o app_wrong_order
```

Вывод:

```text
/usr/bin/ld: main.o: in function `main':
main.cpp:(.text+0x63): undefined reference to `get_lib_version'
/usr/bin/ld: main.cpp:(.text+0xb4): undefined reference to `dot_product'
collect2: error: ld returned 1 exit status
```

Правильный порядок:

```bash
g++ main.o -L. -lmath_dynamic -o app_correct
```

Команда завершилась успешно, без вывода.

- `U` - неразрешенные ссылки,
- `D` - определенные символы,
- `E` - включенные в компоновку файлы. 

При обработке `main.o` файл включается в `E`, определение `main` добавляется в `D`, ссылки на функции библиотеки добавляются в `U`. Следующая за ним библиотека разрешает эти ссылки.

Для `.so` при режиме `--as-needed` библиотека, указанная раньше `main.o`, отбрасывается: нужных ссылок еще нет в `U`. После обработки `main.o` ссылки остаются неразрешенными. Повторная проверка с явным `-Wl,--as-needed` дала те же ошибки. Извлечение отдельных объектных файлов из архива относится к статическим библиотекам.

## 4. Name mangling и extern "C"

После удаления обертки `extern "C"` из заголовка:

```bash
g++ -c main.cpp -o main.o
g++ main.o -L. -lmath_dynamic -o app_no_extern
```

Вывод:

```text
/usr/bin/ld: main.o: in function `main':
main.cpp:(.text+0x63): undefined reference to `get_lib_version()'
/usr/bin/ld: main.cpp:(.text+0xb4): undefined reference to `dot_product(int const*, int const*, int)'
collect2: error: ld returned 1 exit status
```

Команда `nm main.o | grep -E 'dot|get_lib'`:

```text
                 U _Z11dot_productPKiS0_i
                 U _Z15get_lib_versionv
```

Команда `nm libmath_dynamic.so | grep -E 'dot|get_lib'`:

```text
000000000000110a T dot_product
00000000000010f9 T get_lib_version
```

Компилятор C++ кодирует имена функций с учетом типов параметров. Библиотека C содержит обычные имена, поэтому символы не совпадают и линковка завершается ошибкой. Обертка `extern "C"` задает C-связывание и устраняет это несовпадение.

После эксперимента обертка восстановлена, `main.o` пересобран, рабочая программа успешно проверена.
