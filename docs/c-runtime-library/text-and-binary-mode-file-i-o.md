---
description: Дополнительные сведения о файловых операциях ввода-вывода в текстовом и двоичном режиме
title: Файловый ввод-вывод в текстовом и двоичном режиме
ms.date: 04/11/2018
helpviewer_keywords:
- files [C++], open functions
- I/O [CRT], text files
- functions [CRT], file access
- binary access, binary mode file I/O
- translation, modes
- I/O [CRT], binary
- text files, I/O
- I/O [CRT], translation modes
- translation modes (file I/O)
- binary access
ms.assetid: 3196e321-8b87-4609-b302-cd6f3c516051
ms.openlocfilehash: de4e7e7ea1792a23aac3507ec191f3433112b8dc
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97326899"
---
# <a name="text-and-binary-mode-file-io"></a>Файловый ввод-вывод в текстовом и двоичном режиме

Операции файлового ввода-вывода выполняются в одном из двух режимов преобразования: *текстовый* или *двоичный*, в зависимости от режима открытия файла. Файлы данных обычно обрабатываются в текстовом режиме. Для управления режимом преобразования файла можно:

- Сохранить текущий параметр по умолчанию и указывать альтернативный режим только при открытии выбранных файлов.

- С помощью функции [_set_fmode](../c-runtime-library/reference/set-fmode.md) изменить режим по умолчанию для вновь открываемых файлов. С помощью функции [_get_fmode](../c-runtime-library/reference/get-fmode.md) определить текущий режим по умолчанию. Начальная настройка по умолчанию — текстовый режим (**_O_TEXT**).

- Изменить режим преобразования по умолчанию напрямую, определив в программе глобальную переменную [_fmode](../c-runtime-library/fmode.md). Значение этой переменной устанавливается функцией **_set_fmode**, но его можно также задать напрямую.

При вызове функции, открывающей файл, например [_open](../c-runtime-library/reference/open-wopen.md), [fopen](../c-runtime-library/reference/fopen-wfopen.md), [fopen_s](../c-runtime-library/reference/fopen-s-wfopen-s.md), [freopen](../c-runtime-library/reference/freopen-wfreopen.md), [freopen_s](../c-runtime-library/reference/freopen-s-wfreopen-s.md), [_fsopen](../c-runtime-library/reference/fsopen-wfsopen.md) или [_sopen_s](../c-runtime-library/reference/sopen-s-wsopen-s.md), можно переопределить текущее значение по умолчанию для параметра **_fmode**, передав соответствующий аргумент в функцию [_set_fmode](../c-runtime-library/reference/set-fmode.md). Потоки **stdin**, **stdout** и **stderr** по умолчанию всегда открываются в текстовом режиме; можно также переопределить это значение по умолчанию при открытии любого из этих файлов. После открытия файла режим преобразования можно изменить с помощью функции [_setmode](../c-runtime-library/reference/setmode.md), передав ей дескриптора файла.

## <a name="see-also"></a>См. также раздел

[Входные и выходные данные](../c-runtime-library/input-and-output.md)<br/>
[Подпрограммы универсальной среды выполнения C по категориям](../c-runtime-library/run-time-routines-by-category.md)<br/>
