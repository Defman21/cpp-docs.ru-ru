---
description: 'Подробнее о следующем: Библиотеки DLL и поведение библиотеки времени выполнения Visual C++'
title: Библиотеки DLL и поведение библиотеки времени выполнения Visual C++
ms.date: 08/19/2019
f1_keywords:
- _DllMainCRTStartup
- CRT_INIT
helpviewer_keywords:
- DLLs [C++], entry point function
- process detach [C++]
- process attach [C++]
- DLLs [C++], run-time library behavior
- DllMain function
- _CRT_INIT macro
- _DllMainCRTStartup method
- run-time [C++], DLL startup sequence
- DLLs [C++], startup sequence
ms.assetid: e06f24ab-6ca5-44ef-9857-aed0c6f049f2
ms.openlocfilehash: 5b76ec562b87969350b49d38e24c33ce7a4fabf8
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97275455"
---
# <a name="dlls-and-visual-c-run-time-library-behavior"></a>Библиотеки DLL и поведение библиотеки времени выполнения Visual C++

При создании библиотеки динамической компоновки (DLL) с помощью Visual Studio в компоновщик по умолчанию входит библиотека времени выполнения Visual C++ (VCRuntime). VCRuntime содержит код, необходимый для инициализации и завершения исполняемого файла C/C++. При связывании с библиотекой DLL код VCRuntime предоставляет внутреннюю функцию точки входа DLL, называемую `_DllMainCRTStartup`, которая обрабатывает сообщения ОС Windows для библиотеки DLL по присоединению к процессу или потоку или отсоединению от процесса или потока. Функция `_DllMainCRTStartup` выполняет такие важные задачи, как настройка безопасности буфера стека, инициализация и завершение библиотеки времени выполнения C (CRT), а также вызовы конструкторов и деструкторов для статических и глобальных объектов. `_DllMainCRTStartup` также вызывает функции-ловушки для других библиотек, таких как WinRT, MFC и ATL, для выполнения их собственных операций инициализации и завершения. Без этой инициализации CRT и другие библиотеки, а также статические переменные остались бы в неинициализированном состоянии. Те же внутренние процедуры инициализации и завершения VCRuntime вызываются независимо от того, какую библиотеку использует библиотека DLL — статически связанную библиотеку CRT или динамически связанную библиотеку CRT.

## <a name="default-dll-entry-point-_dllmaincrtstartup"></a>Точка входа DLL по умолчанию — _DllMainCRTStartup

В Windows все библиотеки DLL могут содержать необязательную функцию точки входа, обычно называемую `DllMain`, которая вызывается как для инициализации, так и для завершения. Это дает возможность выделять или освобождать дополнительные ресурсы по мере необходимости. Windows вызывает функцию точки входа в четырех ситуациях: присоединение процесса, отсоединение процесса, присоединение потока и отсоединение потока. Когда библиотека DLL загружается в адресное пространство процесса либо при загрузке ее использующего приложения, либо при запросе приложением библиотеки DLL во время выполнения, операционная система создает отдельную копию данных библиотеки DLL. Это называется *присоединением процесса*. *Присоединение потока* происходит, когда процесс, в который загружена библиотека DLL, создает новый поток. *Отсоединение потока* происходит при завершении потока. *Отсоединение процесса* происходит, когда библиотека DLL больше не нужна и освобождается приложением. Операционная система выполняет отдельный вызов точки входа библиотеки DLL для каждого из этих событий, передавая аргумент *reason* для каждого типа события. Например, операционная система отправляет `DLL_PROCESS_ATTACH` в качестве аргумента *reason* для обозначения присоединения процесса.

Библиотека VCRuntime предоставляет функцию точки входа с именем `_DllMainCRTStartup` для обработки операций инициализации и завершения по умолчанию. При присоединении процесса функция `_DllMainCRTStartup` настраивает проверки безопасности буфера, инициализирует CRT и другие библиотеки, инициализирует сведения о типах времени выполнения, инициализирует и вызывает конструкторы для статических и нелокальных данных, инициализирует локальное хранилище потока, увеличивает показания внутреннего статического счетчика для каждого присоединения, а затем вызывает предоставляемую пользователем или библиотекой `DllMain`. При отсоединении процесса функция выполняет эти действия в обратном порядке. Она вызывает `DllMain`, уменьшает показатель внутреннего счетчика, вызывает деструкторы, вызывает функции завершения CRT и зарегистрированные функции `atexit` и уведомляет о завершении все другие библиотеки. Когда показатель счетчика присоединений достигает нуля, функция возвращает `FALSE`, чтобы указать Windows на возможность выгрузки DLL. Функция `_DllMainCRTStartup` вызывается также во время присоединения и отсоединения потока. В этих случаях код VCRuntime не выполняет дополнительную инициализацию или завершение самостоятельно, а просто вызывает `DllMain` для передачи сообщения. Если `DllMain` возвращает `FALSE` из присоединения процесса, что говорит о сбое, `_DllMainCRTStartup` вызывает `DllMain` снова и передает `DLL_PROCESS_DETACH` в качестве аргумента *reason*, а затем выполняет оставшуюся часть процесса завершения.

При создании библиотек DLL в Visual Studio точка входа по умолчанию `_DllMainCRTStartup`, предоставляемая VCRuntime, связывается автоматически. Не нужно указывать функцию точки входа для библиотеки DLL с помощью параметра компоновщика [/ENTRY (символ точки входа)](reference/entry-entry-point-symbol.md).

> [!NOTE]
> Несмотря на то, что с помощью параметра /ENTRY компоновщика можно указать другую функцию точки входа для библиотеки DLL, его использовать не рекомендуется, так как функция точка входа должна будет в том же порядке дублировать все действия, выполняемые `_DllMainCRTStartup`. VCRuntime предоставляет функции, позволяющие дублировать свое поведение. Например, можно вызвать [__security_init_cookie](../c-runtime-library/reference/security-init-cookie.md) сразу же при присоединении процесса для поддержки параметра проверки буфера [/GS (проверка безопасности буфера)](reference/gs-buffer-security-check.md). Можно вызвать функцию `_CRT_INIT`, передавая те же параметры, что и функция точки входа, для выполнения остальных функций инициализации или завершения DLL.

<a name="initializing-a-dll"></a>

## <a name="initialize-a-dll"></a>Инициализация библиотеки DLL

Библиотека DLL может содержать код инициализации, который должен выполняться при загрузке библиотеки DLL. Для выполнения ваших собственных функций инициализации и завершения библиотеки DLL `_DllMainCRTStartup` вызывает функцию с именем `DllMain`, которую вы сами можете указать. У `DllMain` должна быть сигнатура, необходимая для точки входа библиотеки DLL. Функция точки входа по умолчанию `_DllMainCRTStartup` вызывает `DllMain` с использованием тех же параметров, передаваемых Windows. По умолчанию, если вы не предоставите функцию `DllMain`, ее предоставит Visual Studio и свяжет таким образом, чтобы функция `_DllMainCRTStartup` всегда могла что-то вызывать. Это означает, что если вам не нужно инициализировать библиотеку DLL, никаких особых действий при создании библиотеки DLL выполнять не требуется.

Следующая сигнатура используется для `DllMain`:

```cpp
#include <windows.h>

extern "C" BOOL WINAPI DllMain (
    HINSTANCE const instance,  // handle to DLL module
    DWORD     const reason,    // reason for calling function
    LPVOID    const reserved); // reserved
```

Некоторые библиотеки создают для функции `DllMain` программу-оболочку. Например, в обычной библиотеке DLL MFC реализуйте функции-члены `InitInstance` и `ExitInstance` объекта `CWinApp` для выполнения операций инициализации и завершения, требуемых библиотекой DLL. Дополнительные сведения см. в разделе [Инициализация обычных библиотек DLL MFC](#initializing-regular-dlls).

> [!WARNING]
> В отношении операций, выполняемых в точке входа DLL, действуют серьезные ограничения. См. [общие рекомендации](/windows/win32/Dlls/dynamic-link-library-best-practices) для конкретных API-интерфейсов Windows, вызывать которые в `DllMain` небезопасно. Если требуется сделать что-то помимо простейшей инициализации, сделайте это в функции инициализации для DLL. Можно потребовать, чтобы приложения вызывали функцию инициализации после выполнения `DllMain` и перед вызовом любых других функций в библиотеке DLL.

<a name="initializing-non-mfc-dlls"></a>

### <a name="initialize-ordinary-non-mfc-dlls"></a>Инициализация обычных (не MFC) библиотек DLL

Чтобы выполнить собственную инициализацию в обычных (не MFC) библиотеках DLL, использующих предоставленную VCRuntime точку входа `_DllMainCRTStartup`, исходный код библиотеки DLL должен содержать функцию с именем `DllMain`. Следующий код представляет собой базовую схему, показывающую, как может выглядеть определение `DllMain`:

```cpp
#include <windows.h>

extern "C" BOOL WINAPI DllMain (
    HINSTANCE const instance,  // handle to DLL module
    DWORD     const reason,    // reason for calling function
    LPVOID    const reserved)  // reserved
{
    // Perform actions based on the reason for calling.
    switch (reason)
    {
    case DLL_PROCESS_ATTACH:
        // Initialize once for each new process.
        // Return FALSE to fail DLL load.
        break;

    case DLL_THREAD_ATTACH:
        // Do thread-specific initialization.
        break;

    case DLL_THREAD_DETACH:
        // Do thread-specific cleanup.
        break;

    case DLL_PROCESS_DETACH:
        // Perform any necessary cleanup.
        break;
    }
    return TRUE;  // Successful DLL_PROCESS_ATTACH.
}
```

> [!NOTE]
> В более старой документации по Windows SDK говорится, что фактическое имя функции точки входа библиотеки DLL должно быть указано в командной строке компоновщика с помощью параметра /ENTRY. В Visual Studio использовать параметр /ENTRY не нужно, если функции точки входа задано имя `DllMain`. На самом деле, если вы используете параметр/ENTRY и задаете функции точки входа имя, отличное от `DllMain`, инициализация CRT будет проходить неправильно, пока функция точки входа не выполнит же вызовы инициализации, что и `_DllMainCRTStartup`.

<a name="initializing-regular-dlls"></a>

### <a name="initialize-regular-mfc-dlls"></a>Инициализация обычных библиотек DLL MFC

Так как обычные библиотеки DLL MFC содержат объект `CWinApp`, они должны выполнять задачи инициализации и завершения в том же расположении, что и приложение MFC: в функциях-членах `InitInstance` и `ExitInstance` класса, производного от `CWinApp`. Поскольку MFC предоставляет функцию `DllMain`, которая вызывается `_DllMainCRTStartup` для `DLL_PROCESS_ATTACH` и `DLL_PROCESS_DETACH`, создавать собственную функцию `DllMain` не требуется. Предоставляемая MFC функция `DllMain` вызывает `InitInstance` при загрузке библиотеки DLL и `ExitInstance` перед выгрузкой библиотеки DLL.

Обычная библиотека DLL MFC может отслеживать нескольких потоков, вызывая [TlsAlloc](/windows/win32/api/processthreadsapi/nf-processthreadsapi-tlsalloc) и [TlsGetValue](/windows/win32/api/processthreadsapi/nf-processthreadsapi-tlsgetvalue) в своей функции `InitInstance`. Эти функции позволяют библиотеке DLL отслеживать данные конкретного потока.

Если в обычной библиотеке DLL MFC, которая динамически связывается с MFC, используется поддержка MFC OLE, базы данных MFC (или DAO) или сокетов MFC, соответственно, отладочные библиотеки DLL расширения MFC MFCO *версия* D.dll, MFCD *версия* D.dll и MFCN *версия* D.dll (где *версия* — номер версии) связываются автоматически. Необходимо вызвать одну из следующих стандартных функций инициализации для каждой из этих библиотек DLL, используемых в `CWinApp::InitInstance` обычной библиотеки DLL MFC.

|Тип поддержки MFC|Вызываемая функция инициализации|
|-------------------------|-------------------------------------|
|MFC OLE (MFCO *версия* D.dll)|`AfxOleInitModule`|
|База данных MFC (MFCO *версия* D.dll)|`AfxDbInitModule`|
|Сокеты MFC (MFCO *версии* D.dll)|`AfxNetInitModule`|

<a name="initializing-extension-dlls"></a>

### <a name="initialize-mfc-extension-dlls"></a>Инициализация библиотек DLL расширения MFC

Так как в библиотеках DLL расширения MFC нет объекта, производного от `CWinApp` (в отличие от обычных библиотек DLL MFC), в функцию `DllMain`, создаваемую мастером DLL MFC, следует добавить собственный код инициализации и завершения.

Мастер предоставляет следующий код для библиотек DLL расширения MFC. В коде `PROJNAME` является заполнителем для имени проекта.

```cpp
#include "pch.h" // For Visual Studio 2017 and earlier, use "stdafx.h"
#include <afxdllx.h>

#ifdef _DEBUG
#define new DEBUG_NEW
#undef THIS_FILE
static char THIS_FILE[] = __FILE__;
#endif
static AFX_EXTENSION_MODULE PROJNAMEDLL;

extern "C" int APIENTRY
DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved)
{
   if (dwReason == DLL_PROCESS_ATTACH)
   {
      TRACE0("PROJNAME.DLL Initializing!\n");

      // MFC extension DLL one-time initialization
      AfxInitExtensionModule(PROJNAMEDLL,
                                 hInstance);

      // Insert this DLL into the resource chain
      new CDynLinkLibrary(Dll3DLL);
   }
   else if (dwReason == DLL_PROCESS_DETACH)
   {
      TRACE0("PROJNAME.DLL Terminating!\n");
   }
   return 1;   // ok
}
```

При создании `CDynLinkLibrary` объекта во время инициализации библиотека DLL расширения MFC может экспортировать объекты `CRuntimeClass` или ресурсы в клиентское приложение.

Если вы собираетесь использовать библиотеку DLL расширения MFC из одной или нескольких обычных библиотек DLL MFC, необходимо экспортировать функцию инициализации, которая создает объект `CDynLinkLibrary`. Эта функция должна вызываться из каждой обычной библиотеки DLL MFC, использующей библиотеку DLL расширения MFC. Подходящим местом для вызова этой функции инициализации является функция-член `InitInstance` объекта библиотеки DLL MFC, производного от `CWinApp`. Вызов следует выполнить до использования экспортированных классов или функций библиотеки DLL расширения MFC.

В функции `DllMain`, создаваемой мастером DLL MFC, вызов `AfxInitExtensionModule` записывает классы среды выполнения модуля (структуры `CRuntimeClass`), а также фабрики объектов (объекты `COleObjectFactory`) для использования при создании объекта `CDynLinkLibrary`. Следует проверить возвращаемое значение `AfxInitExtensionModule`. Если из `AfxInitExtensionModule` возвращается нулевое значение, из функции `DllMain` возвращается нуль.

Если библиотека DLL расширения MFC будет явно связана с исполняемым файлом (то есть исполняемый файл вызывает `AfxLoadLibrary` для связи с библиотекой DLL), необходимо добавить вызов `AfxTermExtensionModule` в `DLL_PROCESS_DETACH`. Эта функция позволяет MFC очищать библиотеку DLL расширения MFC при отсоединении каждого процесса от библиотеки DLL расширения MFC (что происходит при завершении процесса или при выгрузке библиотеки DLL в результате вызова `AfxFreeLibrary`). Если библиотека DLL расширения MFC будет связана с приложением неявным образом, вызывать `AfxTermExtensionModule` не требуется.

Приложения, которые связываются с библиотеками DLL расширения MFC явным образом, должны вызывать `AfxTermExtensionModule` при освобождении библиотеки DLL. Если приложения используют несколько потоков, они также должны использовать `AfxLoadLibrary` и `AfxFreeLibrary` (вместо функций Win32 `LoadLibrary` и `FreeLibrary`). Использование `AfxLoadLibrary` и `AfxFreeLibrary` гарантирует, что код запуска и завершения работы, выполняемый при загрузке и выгрузке библиотеки DLL расширения MFC, не нарушает глобальное состояние MFC.

Так как MFCx0.dll полностью инициализируется к моменту вызова `DllMain`, можно выделить память и вызвать функции MFC в `DllMain` (в отличие от 16-разрядной версии MFC).

Библиотеки DLL расширения могут поддерживать многопоточность, обрабатывая случаи `DLL_THREAD_ATTACH` и `DLL_THREAD_DETACH` в функции `DllMain`. Эти случаи передаются в `DllMain` при присоединении и отсоединении потоков от библиотеки DLL. Вызов [TlsAlloc](/windows/win32/api/processthreadsapi/nf-processthreadsapi-tlsalloc) при присоединении библиотеки DLL позволяет ей поддерживать индексы локального хранилища потока (TLS) для каждого присоединенного потока.

Обратите внимание, что файл заголовка Afxdllx.h содержит специальные определения структур, используемых в библиотеках DLL расширения MFC, например определение для `AFX_EXTENSION_MODULE` и `CDynLinkLibrary`. Этот файл следует включить в библиотеку DLL расширения MFC.

> [!NOTE]
> Важно не определять и не отменять определение макросов `_AFX_NO_XXX` в файле *pch.h* (*stdafx.h* в Visual Studio 2017 и более ранних версиях). Эти макросы существуют, только чтобы проверить, поддерживает ли конкретная целевая платформа эту функцию или нет. Можно написать собственную программу для проверки этих макросов (например, `#ifndef _AFX_NO_OLE_SUPPORT`), но она не должна определять и отменять определение этих макросов.

Пример функции инициализации, обрабатывающей многопоточность, включен в раздел [Использование локального хранилища потока в библиотеке динамической компоновки](/windows/win32/Dlls/using-thread-local-storage-in-a-dynamic-link-library) в Windows SDK. Обратите внимание, что пример содержит функцию точки входа с именем `LibMain`, но ей следует задать имя `DllMain`, чтобы она работала с библиотеками MFC и времени выполнения C.

## <a name="see-also"></a>См. также

[Создание библиотек DLL C/C++ в Visual Studio](dlls-in-visual-cpp.md)<br/>
[Точка входа DllMain](/windows/win32/Dlls/dllmain)<br/>
[Рекомендации по использованию библиотеки динамической компоновки](/windows/win32/Dlls/dynamic-link-library-best-practices)
