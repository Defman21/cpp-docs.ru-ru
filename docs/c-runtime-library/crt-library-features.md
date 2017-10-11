---
title: "Особенности библиотеки CRT | Документы Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- c.runtime
dev_langs:
- C++
helpviewer_keywords:
- MSVCR71.dll
- libraries [C++], multithreaded
- library files, run-time
- LIBCMT.lib
- LIBCP.lib
- LIBCPMT.lib
- run-time libraries, C
- CRT, release versions
- MSVCP71.dll
- LIBC.lib
- libraries [C++]
- libraries [C++], run-time
- linking [C++], libraries
ms.assetid: a889fd39-807d-48f2-807f-81492612463f
caps.latest.revision: 32
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 22da7776e46171467a37d46c3de3227f060eaf77
ms.openlocfilehash: 0ae005c2367f891e0b7a91e3f7e45d42d852fb78
ms.contentlocale: ru-ru
ms.lasthandoff: 08/11/2017

---
# <a name="crt-library-features"></a>Особенности библиотеки CRT
В этом разделе обсуждаются различные LIB-файлы, входящие в библиотеки времени выполнения C, а также связанные параметры компилятора и директивы препроцессора.  
  
## <a name="c-run-time-libraries-crt"></a>Библиотеки среды выполнения C (CRT)  
 Библиотека времени выполнения C (CRT) является частью стандартной библиотеки C++, содержащей библиотеку C99 стандарта ISO. Библиотеки Visual C++, которые реализуют CRT, поддерживают разработку с использованием машинного кода, сочетания машинного и управляемого кода, а также полностью управляемого кода для разработки в среде .NET. Все версии библиотек CRT поддерживают разработку многопоточного кода. Большинство библиотек поддерживает как статическое связывание (для связывания библиотеки непосредственно в коде), так и динамическое связывание (для использования в коде общих библиотек DLL).  
  
 Начиная с Visual Studio 2015, был проведен рефакторинг CRT, повлекший создание новых двоичных файлов. Универсальная библиотека CRT (UCRT) содержит функции и глобальные переменные, экспортируемые стандартной библиотекой CRT C99. UCRT теперь является компонентом Windows и поставляется в составе Windows 10. Статическая библиотека, DLL-библиотека импорта и файлы заголовков для UCRT теперь входят в пакет SDK для Windows 10. При установке Visual C++ программа установки Visual Studio устанавливает набор компонентов из пакета SDK для Windows 10, необходимых для использования UCRT. Библиотеку UCRT можно использовать в любой версии Windows, поддерживаемой Visual Studio 2015 и более поздними версиями. Ее можно распространять с помощью vcredist для поддерживаемых версий Windows (кроме Windows 10). Дополнительные сведения см. в разделе [Redistributing Visual C++ Files](../ide/redistributing-visual-cpp-files.md).  
  
 В следующей таблице перечислены библиотеки, которые реализуют UCRT.  
  
|Библиотека|Связанная DLL|Характеристики|Параметр|Директивы препроцессора|  
|-------------|--------------------|---------------------|------------|-----------------------------|  
|libucrt.lib|Нет|Статически связывает UCRT в коде.|**/MT**|_MT|  
|libucrtd.lib|Нет|Отладочная версия UCRT для статического связывания. Нераспространяемый компонент.|**/MTd**|_DEBUG, _MT|  
|ucrt.lib|ucrtbase.dll|DLL-библиотека импорта для UCRT.|**/MD**|_MT, _DLL|  
|ucrtd.lib|ucrtbased.dll|DLL-библиотека импорта для отладочной версии UCRT. Нераспространяемый компонент.|**/MDd**|_DEBUG, _MT, _DLL|  
  
 Библиотека vcruntime содержит код Visual C++, определяемый реализацией CRT (такой как поддержка обработки исключений и отладки), проверки времени выполнения, сведения о типах, сведения о реализации и некоторые расширенные функции библиотеки. Эта библиотека определяется версией используемого компилятора.  
  
 В этой таблице перечислены библиотеки, которые реализуют библиотеку vcruntime.  
  
|Библиотека|Связанная DLL|Характеристики|Параметр|Директивы препроцессора|  
|-------------|--------------------|---------------------|------------|-----------------------------|  
|libvcruntime.lib|Нет|Статически связанная с кодом.|**/MT**|_MT|  
|libvcruntimed.lib|Нет|Отладочная версия для статического связывания. Нераспространяемый компонент.|**/MTd**|_MT, _DEBUG|  
|vcruntime.lib|vcruntime\<version>.dll|DLL-библиотека импорта для vcruntime.|**/MD**|_MT, _DLL|  
|vcruntimed.lib|vcruntime\<version>d.dll|DLL-библиотека импорта для отладочной версии vcruntime. Нераспространяемый компонент.|**/MDd**|_DEBUG, _MT, _DLL|  
  
 Код, инициализирующий CRT, находится в одной из нескольких библиотек в зависимости от статического или динамического связывания библиотеки CRT и использования машинного, управляемого или смешанного кода. Этот код обрабатывает запуск, инициализацию внутренних данных потоков и завершение CRT. Он определяется версией используемого компилятора. Эта библиотека всегда статически связана, даже при использовании динамически связанной библиотеки UCRT.  
  
 В этой таблице перечислены библиотеки, которые реализуют инициализацию и завершение CRT.  
  
|Библиотека|Характеристики|Параметр|Директивы препроцессора|  
|-------------|---------------------|------------|-----------------------------|  
|LIBCMT.lib|Статически связывает в коде запуск CRT машинного кода.|**/MT**|_MT|  
|libcmtd.lib|Статически связывает отладочную версию запуска CRT в машинном коде. Нераспространяемый компонент.|**/MTd**|_DEBUG, _MT|  
|msvcrt.lib|Статическая библиотека для запуска CRT в машинном коде для использования с DLL, UCRT и vcruntime.|**/MD**|_MT, _DLL|  
|msvcrtd.lib|Статическая библиотека для запуска отладочной версии CRT в машинном коде для использования с DLL, UCRT и vcruntime. Нераспространяемый компонент.|**/MDd**|_DEBUG, _MT, _DLL|  
|msvcmrt.lib|Статическая библиотека для запуска CRT в смешанном машинном и управляемом коде для использования с DLL, UCRT и vcruntime.|**/clr**||  
|msvcmrtd.lib|Статическая библиотека для запуска отладочной версии CRT в смешанном машинном и управляемом коде для использования с DLL, UCRT и vcruntime. Нераспространяемый компонент.|**/clr**||  
|msvcurt.lib|**Нерекомендуемая** статическая библиотека для CRT с полностью управляемым кодом.|**/clr:pure**||  
|msvcurtd.lib|**Нерекомендуемая** статическая библиотека для отладочной версии CRT с полностью управляемым кодом. Нераспространяемый компонент.|**/clr:pure**||  
  
 При ссылке программы из командной строки без параметра компилятора, задающего библиотеку выполнения C, компоновщик будет использовать статически связанные библиотеки CRT: libcmt.lib, libvcruntime.lib и libucrt.lib.  
  
 Использование статически скомпонованных CRT означает, что все сведения о состоянии, сохраненные библиотекой времени выполнения C, будут локальны по отношению к этому экземпляру CRT. Например, если применяется [strtok, _strtok_l, wcstok, _wcstok_l, _mbstok, _mbstok_l](../c-runtime-library/reference/strtok-strtok-l-wcstok-wcstok-l-mbstok-mbstok-l.md) при использовании статически скомпонованной CRT, позиция анализатора `strtok` не связана с состоянием `strtok`, которое используется в коде в этом же процессе (но в другом файле DLL или EXE), скомпонованном с другим экземпляром статической библиотеки CRT. Напротив, динамически скомпонованная библиотека CRT позволяет использовать состояние всему коду в процессе, который динамически скомпонован с этой библиотекой CRT. Это не относится к новым более безопасным версиям этих функций; например, эта проблема не распространяется на `strtok_s` .  
  
 Поскольку библиотека DLL, собранная путем компоновки со статической библиотекой CRT, будет иметь собственное состояние CRT, не рекомендуется использовать статическую компоновку с CRT для DLL без понимания последствий и конкретной необходимости. Например, при вызове функции [_set_se_translator](../c-runtime-library/reference/set-se-translator.md) в исполняемом файле, который загружает библиотеку DLL, скомпонованную с собственной статической библиотекой CRT, все аппаратные исключения, создаваемые в коде библиотеки DLL, не будут перехватываться транслятором, в отличие от аппаратных исключений, создаваемых в коде основного исполняемого файла.  
  
 Если используется параметр компилятора **/clr** , код будет скомпонован со статической библиотекой msvcmrt.lib. Эта статическая библиотека предоставляет функцию прокси между управляемым кодом и неуправляемой средой CRT. Невозможно использовать статически скомпонованные CRT (параметры **/MT** или **/MTd** ) с параметром **/clr**. Вместо этого используйте динамически скомпонованные библиотеки (**/MD** или **/MDd**).  
  
 Если используется параметр компилятора **/clr:pure** , код будет скомпонован со статической библиотекой msvcurt.lib. Как и в случае параметра **/clr**, компоновка со статически скомпонованной библиотекой не допускается. Начиная с Visual Studio 2015, не рекомендуется использовать параметры компилятора **/clr:pure** и **/clr:safe**.  
  
 Дополнительные сведения об использовании CRT с **/clr** см. в разделе [Смешанные (собственные и управляемые) сборки](../dotnet/mixed-native-and-managed-assemblies.md); если используется **/clr:pure**, см. дополнительные сведения в разделе [Чистый и проверяемый код (C++/CLI)](../dotnet/pure-and-verifiable-code-cpp-cli.md).  
  
 Для сборки отладочной версии приложения должен быть определен флаг [_DEBUG](../c-runtime-library/debug.md), и приложение должно быть скомпоновано с отладочной версией одной из этих библиотек. Дополнительные сведения об использовании отладочных версий файлов библиотек см. в разделе [Методы отладки CRT](/visualstudio/debugger/crt-debugging-techniques).  
  
 Эта версия CRT не полностью совместима со стандартом C99. В частности, заголовок \<tgmath.h> и макросы pragma CX_LIMITED_RANGE/FP_CONTRACT не поддерживаются. Некоторые элементы, такие как значения спецификаторов параметров в стандартных функциях ввода-вывода, по умолчанию используют интерпретации прежних версий. Для управления некоторыми аспектами соответствия библиотеки можно использовать параметры согласованности компилятора /Zc и задать параметры компоновщика.  
  
## <a name="c-standard-library"></a>Стандартная библиотека C++  
  
|Стандартная библиотека C++|Характеристики|Параметр|Директивы препроцессора|  
|----------------------------|---------------------|------------|-----------------------------|  
|LIBCPMT.lib|Многопоточная, статическая компоновка.|**/MT**|_MT|  
|MSVCPRT.LIB|Многопоточная, динамическое связывание (библиотека импорта для MSVCP\<version>.dll)|**/MD**|_MT, _DLL|  
|LIBCPMTD.LIB|Многопоточная, статическая компоновка.|**/MTd**|_DEBUG, _MT|  
|MSVCPRTD.LIB|Многопоточная, динамическое связывание (библиотека импорта для MSVCP\<version>D.DLL)|**/MDd**|_DEBUG, _MT, _DLL|  
  
 При сборке финальной версии проекта одна из базовых библиотек времени выполнения C (LIBCMT.LIB, MSVCMRT.LIB, MSVCRT.LIB) будет скомпонована по умолчанию, в зависимости от выбранного параметра компилятора (многопоточный, DLL, /clr). Если вы включите в код любой из [файлов заголовка стандартной библиотеки C++](../standard-library/cpp-standard-library-header-files.md), Visual C++ автоматически подключит стандартную библиотеку C++ во время компиляции. Пример:  
  
```  
#include <ios>   
```  
  
## <a name="what-problems-exist-if-an-application-uses-more-than-one-crt-version"></a>Если приложение использует несколько версий CRT, с какими проблемами можно столкнуться?  
 Если у вас есть несколько файлов DLL или EXE, вы можете использовать несколько CRT при любых сочетаниях версий Visual C++. Например, статическая компоновка библиотеки CRT с несколькими библиотеками DLL может представлять такую же проблему. Разработчики, которые столкнулись с этой проблемой со статическими CRT, получили инструкции компилировать с параметром **/MD** для использования CRT DLL. Если библиотеки DLL передают ресурсы CRT через границы DLL, могут возникнуть проблемы несоответствия библиотек CRT и потребуется выполнить повторную компиляцию проекта с помощью Visual C++.  
  
 Если программа использует несколько версий CRT, необходимо быть осторожным при передаче некоторых объектов CRT (например, дескрипторов файлов, языковых стандартов и переменных среды) через границы библиотеки DLL. Дополнительные сведения о связанных проблемах и способах их устранения см. в разделе [Потенциальные ошибки при передаче объектов CRT через границы DLL](../c-runtime-library/potential-errors-passing-crt-objects-across-dll-boundaries.md).  
  
## <a name="see-also"></a>См. также  
 [Справочник по библиотеке времени выполнения C](../c-runtime-library/c-run-time-library-reference.md)