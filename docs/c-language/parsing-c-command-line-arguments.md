---
title: Анализ аргументов командной строки C
description: Узнайте, как код запуска среды выполнения Microsoft C интерпретирует аргументы командной строки при создании параметров argv и argc.
ms.date: 11/09/2020
helpviewer_keywords:
- quotation marks, command-line arguments
- double quotation marks
- double quote marks
- command line, parsing
- parsing, command-line arguments
- startup code, parsing command-line arguments
ms.assetid: ffce8037-2811-45c4-8db4-1ed787859c80
ms.openlocfilehash: 92921e91ee6bb37b2bf7b702a1b31ed045187b59
ms.sourcegitcommit: b38485bb3a9d479e0c5d64ffc3d841fa2c2b366f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2020
ms.locfileid: "94441259"
---
# <a name="parsing-c-command-line-arguments"></a>Анализ аргументов командной строки C

**Блок, относящийся только к системам Microsoft**

В коде запуска Microsoft C используются следующие правила при обработке аргументов, вводимых в командной строке операционной системы.

- Аргументы разделяются пробелами (пробел или табуляция).

- Первый аргумент (`argv[0]`) обрабатывается особым образом. Он представляет имя программы. Это должен быть допустимый путь, поэтому разрешены части, заключенные в двойные кавычки ( **`"`** ). Эти знаки двойных кавычек не включаются в выходные данные `argv[0]`. Заключение частей в двойные кавычки не позволяет интерпретировать пробел или символ табуляции как конец аргумента. Последующие правила в этом списке не применяются.

- Строка, заключенная в двойные кавычки, обрабатывается как один аргумент независимо от наличия в ней пробелов. Строку в кавычках можно встроить в аргумент. Символ каретки ( **`^`** ) не распознается как escape-символ или разделитель. Внутри заключенной в кавычки строки пара двойных кавычек интерпретируется как одна экранированная двойная кавычка. Если командная строка заканчивается раньше, чем будет найдена закрывающая двойная кавычка, все уже прочитанные символы выводятся как один последний аргумент.

- Символ двойной кавычки после обратной косой черты ( **`\"`** ) интерпретируется как литеральный символ двойной кавычки ( **`"`** ).

- Символы обратной косой черты считаются литералами, если сразу за ними не стоит двойная кавычка.

- Если двойная кавычка стоит после четного числа символов обратной косой черты, в массив `argv` помещается по одному символу обратной косой черты ( **`\`** ) для каждой пары символов обратной косой черты ( **`\\`** ), а сама двойная кавычка ( **`"`** ) интерпретируется как разделитель строк.

- Если двойная кавычка стоит после нечетного числа символов обратной косой черты, в массив `argv` помещается по одному символу обратной косой черты ( **`\`** ) для каждой пары символов обратной косой черты ( **`\\`** ). Сам знак двойной кавычки в этом случае интерпретируется как escape-последовательность в сочетании с последним символом обратной косой черты, то есть в `argv` помещается литерал двойной кавычки ( **`"`** ).

В следующем списке, иллюстрирующем указанные выше правила, показаны результаты, передаваемые в массив `argv` для нескольких примеров аргументов командной строки. Выходные данные, представленный во втором, третьем и четвертом столбцах, получены из программы ARGS.C, приведенной после списка.

|Данные в командной строке|argv[1]|argv[2]|argv[3]|
|-------------------------|---------------|---------------|---------------|
|`"a b c" d e`|`a b c`|`d`|`e`|
|`"ab\"c" "\\" d`|`ab"c`|`\`|`d`|
|`a\\\b d"e f"g h`|`a\\\b`|`de fg`|`h`|
|`a\\\"b c d`|`a\"b`|`c`|`d`|
|`a\\\\"b c" d e`|`a\\b c`|`d`|`e`|
|`a"b"" c d`|`ab" c d`|||

## <a name="example"></a>Пример

### <a name="code"></a>Код

```c
// ARGS.C illustrates the following variables used for accessing
// command-line arguments and environment variables:
// argc  argv  envp
//

#include <stdio.h>

int main( int argc, // Number of strings in array argv
char *argv[],      // Array of command-line argument strings
char **envp )      // Array of environment variable strings
{
    int count;

    // Display each command-line argument.
    printf_s( "\nCommand-line arguments:\n" );
    for( count = 0; count < argc; count++ )
        printf_s( "  argv[%d]   %s\n", count, argv[count] );

    // Display each environment variable.
    printf_s( "\nEnvironment variables:\n" );
    while( *envp != NULL )
        printf_s( "  %s\n", *(envp++) );

    return;
}
```

## <a name="comments"></a>Комментарии

Ниже приведен один пример данных, выводимых этой программой:

```
Command-line arguments:
  argv[0]   C:\MSC\TEST.EXE

Environment variables:
  COMSPEC=C:\NT\SYSTEM32\CMD.EXE

  PATH=c:\nt;c:\binb;c:\binr;c:\nt\system32;c:\word;c:\help;c:\msc;c:\;
  PROMPT=[$p]
  TEMP=c:\tmp
  TMP=c:\tmp
  EDITORS=c:\binr
  WINDIR=c:\nt
```

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[Функция main и выполнение программ](../c-language/main-function-and-program-execution.md)
