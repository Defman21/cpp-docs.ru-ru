---
description: 'Подробнее о следующем: Распространенные проблемы, возникающие при создании построений выпуска'
title: Распространенные проблемы, возникающие при создании построений выпуска
ms.date: 11/04/2016
helpviewer_keywords:
- unexpected code generation
- debugging [MFC], release builds
- release builds, troubleshooting
- stray pointers
- debug builds, difference from release builds
- MFC [C++], release builds
- heap layout problems
- pointers, stray
- release builds, building applications
- debug memory allocator
- optimization [C++], compiler
- projects [C++], debug configuration
- troubleshooting release builds
- memory [C++], overwrites
ms.assetid: 73cbc1f9-3e33-472d-9880-39a8e9977b95
ms.openlocfilehash: 7470b87a33b9dc0cb6f7e85b9cfa7b7c1216a936
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97163097"
---
# <a name="common-problems-when-creating-a-release-build"></a>Распространенные проблемы, возникающие при создании построений выпуска

Как правило, во время разработки процессы сборки и тестирования выполняются с помощью отладочной сборки проекта. Если затем требуется собрать приложение для сборки выпуска, может возникнуть нарушение доступа.

Далее показаны основные различия между отладочной сборкой и сборкой выпуска. Существуют и другие различия, но ниже приведены основные различия, которые могут привести к сбою приложения в сборке выпуска, когда оно работает в отладочной сборке.

- [Макет кучи](#_core_heap_layout)

- [Компиляция](#_core_compilation)

- [Поддержка указателей](#_core_pointer_support)

- [Оптимизации](#_core_optimizations)

Сведения о перехвате ошибок сборки выпуска в отладочных сборках см. в статье о параметре компилятора [/GZ (перехват ошибок сборки в отладочной сборке)](reference/gz-enable-stack-frame-run-time-error-checking.md).

## <a name="heap-layout"></a><a name="_core_heap_layout"></a>Макет кучи

Макет кучи будет причиной примерно 90 % очевидных проблем при работе приложения в режиме отладки, но не в режиме выпуска.

При сборке проекта для отладки используется механизм распределения отладочной памяти. Это значит, что все блоки выделенной памяти заключаются в последовательности защитных байтов. Эти байты обнаруживают перезапись памяти. Поскольку в версиях выпуска и отладки используются разные макеты кучи, перезапись памяти может не приводить к проблемам в отладочной сборке, но может иметь катастрофические последствия в сборке выпуска.

Дополнительные сведения см. в статьях [Проверка перезаписи памяти](checking-for-memory-overwrites.md) и [Использование отладочной сборки для проверки перезаписи памяти](using-the-debug-build-to-check-for-memory-overwrite.md).

## <a name="compilation"></a><a name="_core_compilation"></a> Компиляция

При создании сборки выпуска происходит изменение многих макросов MFC и большей части реализации MFC. В частности, макрос ASSERT ничего не возвращает в сборке выпуска, поэтому никакие фрагменты кода в ASSERT выполняться не будут. Дополнительные сведения см. в статье о [проверке операторов ASSERT](using-verify-instead-of-assert.md).

Некоторые функции встроены для повышения скорости в сборке выпуска. Оптимизации обычно активированы в сборке выпуска. Также используется другой механизм распределения памяти.

## <a name="pointer-support"></a><a name="_core_pointer_support"></a> Поддержка указателей

Отсутствие отладочной информации удаляет заполнение из приложения. В сборке выпуска лишние указатели с большей вероятностью могут указывать на неинициализированную память, чем на отладочную информацию.

## <a name="optimizations"></a><a name="_core_optimizations"></a> Оптимизации

В зависимости от характера определенных сегментов кода оптимизирующий компилятор может генерировать непредвиденный код. Это наименее вероятная причина проблем сборки выпуска, однако она иногда тоже может возникать. Сведения о решении см. в статье [Оптимизация кода](optimizing-your-code.md).

## <a name="see-also"></a>См. также

[Сборки выпуска](release-builds.md)<br/>
[Устранение проблем сборки выпуска](fixing-release-build-problems.md)
