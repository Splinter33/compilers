# Отчет по лабораторной работе 2

## 1. Размеры секций

Команда: `size core.o legacy.o hotfix.o main.o`.

```text
text    data    bss    dec    hex   filename
266     4040  50000  54306   d422   core.o
172        0      4    176     b0   legacy.o
127        0      0    127     7f   hotfix.o
118        0      0    118     76   main.o
```

## 2. Большая секция .bss

В `core.o` массив `large_buffer` занимает 50000 байт в `.bss`, хотя размер файла по `ls -l` составляет 6200 байт. Секция имеет тип `NOBITS`: ее содержимое не хранится на диске, память выделяется и обнуляется при загрузке. Столбец `dec` показывает сумму размеров секций, а не размер файла на диске.

## 3. Секция со строками

Команды: `readelf -SW core.o`, `readelf -SW legacy.o`, `readelf -SW hotfix.o`.

В `core.o` найдена секция `.rodata`, отсутствующая в двух других файлах:

```text
[ 5] .rodata PROGBITS 0000000000000000 001048 00004c 00 A 0 0 16
```

## 4. Секретный токен

Команда: `strings -a core.o`. Значимые строки:

```text
System Initialized v1.0
FLAG{b1nary_4rch4eology_2026}
%s, Mode: %d
```

Токен: `FLAG{b1nary_4rch4eology_2026}`.

## 5. Общие имена

Команда: `nm -A core.o legacy.o hotfix.o main.o`.

Повторяются `system_mode`, `print_status`, `apply_hotfix`:

```text
core.o:0000000000000012 T print_status
core.o:0000000000000000 D system_mode
legacy.o:0000000000000004 C system_mode
hotfix.o:0000000000000000 T apply_hotfix
hotfix.o:0000000000000004 C system_mode
main.o:                 U apply_hotfix
main.o:                 U print_status
```

## 6. Типы и секции общих символов

Данные получены командами `nm -A` и `readelf -sW core.o legacy.o hotfix.o main.o`.

| Символ | Файл | Тип nm | Ndx | Секция |
|---|---|---|---|---|
| system_mode | core.o | D | 3 | .data |
| system_mode | legacy.o | C | COM | COMMON |
| system_mode | hotfix.o | C | COM | COMMON |
| print_status | core.o | T | 1 | .text |
| print_status | main.o | U | UND | Не определен |
| apply_hotfix | hotfix.o | T | 1 | .text |
| apply_hotfix | main.o | U | UND | Не определен |

COMMON не является обычной секцией объектного файла. Эти символы имеют привязку GLOBAL, а не WEAK.

## 7. Конфликт system_mode

По `readelf -sW` размер `system_mode` во всех трех модулях равен 4 байтам. В `core.o` переменная определена в `.data`, в `legacy.o` и `hotfix.o` представлена COMMON-символом. В `hotfix.c` это `char[4]`. Точный C-тип в остальных модулях по таблице символов установить нельзя. Выравнивание COMMON-символа в `legacy.o` равно 4, в `hotfix.o` - 1. Объединение имени может привести к несовместимому использованию одной области памяти; одинаковый размер не гарантирует одинаковые типы.

## 8. Первая компоновка

```bash
gcc -fcommon core.o legacy.o hotfix.o main.o -o app
```

Сборка прошла без ошибок и предупреждений. Определение из `core.o` имеет приоритет над COMMON-символами. Компоновщик не проверяет совместимость C-типов по обычной таблице символов.

## 9. Символ в исполняемом файле

Команда: `nm -S app | grep system_mode`.

```text
0000000000004020 0000000000000004 D system_mode
```

Команда: `readelf -sW app | grep system_mode`.

```text
33: 0000000000004020 4 OBJECT GLOBAL DEFAULT 25 system_mode
```

Символ находится в `.data`, поскольку выбрано определение из `core.o`.

## 10. Запрет COMMON и исправление

```bash
gcc -fno-common main.o hotfix.o legacy.o core.o -o app_better
```

Команда из задания завершилась без сообщений. Флаг `-fno-common` не изменяет готовые объектные файлы. Для проверки создан `hotfix.c` по коду с задания и выполнена пересборка:

```bash
gcc -fno-common -c hotfix.c -o hotfix_nocommon.o &&
gcc main.o hotfix_nocommon.o legacy.o core.o -o app_better
```

Вывод:

```text
/usr/bin/ld: warning: alignment 1 of normal symbol `system_mode' in hotfix_nocommon.o is smaller than 4 used by the common definition in legacy.o
/usr/bin/ld: warning: NOTE: alignment discrepancies can cause real problems.  Investigation is advised.
/usr/bin/ld: core.o:(.data+0x0): multiple definition of `system_mode'; hotfix_nocommon.o:(.bss+0x0): first defined here
collect2: error: ld returned 1 exit status
```

После пересборки `hotfix.c` содержит обычное определение в `.bss`, которое конфликтует с определением в `.data` из `core.o`.

Исправление без изменения имени:

```c
static char system_mode[4];
```

После замены объявления повторная компиляция и компоновка теми же командами прошли без сообщений. `static` задает внутреннее связывание и устраняет конфликт. Теперь hotfix изменяет собственную переменную. Если требуется изменять общую переменную, необходимо согласовать ее тип между модулями и использовать `extern` при единственном определении.