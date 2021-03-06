---
title: Практическое руководство. Использование существующего кода C++ в приложении универсальной платформы Windows
description: Способы использования существующих приложений и библиотек кода в универсальная платформа Windows приложениях.
ms.date: 09/04/2020
ms.assetid: 87e5818c-3081-42f3-a30d-3dca2cf0645c
ms.openlocfilehash: fd23c875d67654e96a828f4dba412dd74652912a
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2020
ms.locfileid: "91503671"
---
# <a name="how-to-use-existing-c-code-in-a-universal-windows-platform-app"></a>Практическое руководство. Использование существующего кода C++ в приложении универсальной платформы Windows

Существует множество способов использования существующего кода C++ в проектах универсальная платформа Windows (UWP). Некоторые способы не нуждаются в повторной компиляции кода с включенными расширениями компонентов (C++/CX) (то есть с `/ZW` параметром), а также с некоторыми возможностями. Может потребоваться сохранить код в стандартном C++ или сохранить классическую среду компиляции Win32 для некоторого кода. Вы по-прежнему можете сделать это, используя соответствующие варианты архитектуры. Рассмотрим весь код, содержащий пользовательский интерфейс и типы UWP, которые доступны для вызовов C#, Visual Basic и JavaScript. Этот код должен находиться в проектах приложений Windows и проектах компонентов среда выполнения Windows. Код, который вызывается только из C++ (включая C++/CX), может быть в проекте, который компилируется с `/ZW` параметром или стандартным проектом C++. Двоичный код, который не использует запрещенные API-интерфейсы, можно использовать, связав его в качестве статической библиотеки. Вы также можете упаковать его с приложением как содержимое и загрузить в библиотеку DLL.

Возможно, самым простым способом запуска классической программы в среде UWP является использование технологий Desktop Bridge. Они включают в себя преобразователь для классических приложений, который будет упаковывать существующее приложение как приложение UWP без необходимости вносить изменения в код. Дополнительные сведения см. в статье [Мост для классических приложений](/windows/uwp/porting/desktop-to-uwp-root).

В оставшейся части этой статьи описывается, как перенести библиотеки C++ (библиотеки DLL и статические библиотеки) в универсальная платформа Windows. Вам может потребоваться перенести код так, чтобы Базовая логика C++ могла использоваться с несколькими приложениями UWP.

Приложения UWP выполняются в защищенной среде. В результате многих вызовов API Win32, COM и CRT, которые могут поставить под угрозу безопасность платформы, не допускаются. `/ZW`Параметр компилятора может обнаруживать такие вызовы и формировать ошибку. Вы можете использовать комплект сертификации приложений для определения кода, который вызывает запрещенные API. Дополнительные сведения см. в разделе [Тесты комплекта сертификации приложений для Windows](/windows/uwp/debug-test-perf/windows-app-certification-kit).

Если исходный код доступен для библиотеки, можно попытаться исключить недопустимые вызовы API. Список недопустимых API см. в разделе [API Win32 и com для приложений UWP](/uwp/win32-and-com/win32-and-com-for-uwp-apps) и [функций CRT, которые не поддерживаются в универсальная платформа Windows приложениях](../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md). Некоторые альтернативные решения можно найти в статье [Альтернативы Windows API для приложений среды выполнения Windows](/uwp/win32-and-com/alternatives-to-windows-apis-uwp).

Если вы просто пытаетесь добавить ссылку из универсального проекта Windows в классическую библиотеку настольных систем, появится сообщение об ошибке, сообщающее о несовместимости библиотеки. Если это статическая библиотека, можно создать ссылку на библиотеку, добавив библиотеку ( *`.lib`* файл) в входные данные компоновщика так же, как в классическом приложении Win32. Если доступна только двоичная Библиотека, это единственный вариант. Статическая библиотека связана с исполняемым файлом приложения. Однако библиотека DLL Win32, используемая в приложении UWP, должна быть упакована в приложение, включая его в проект и помечая как содержимое. Чтобы загрузить библиотеку DLL Win32 в приложении UWP, необходимо также вызвать метод [`LoadPackagedLibrary`](/windows/win32/api/winbase/nf-winbase-loadpackagedlibrary) вместо `LoadLibrary` или `LoadLibraryEx` .

При наличии исходного кода библиотеки DLL или статической библиотеки ее можно перекомпилировать как проект UWP с помощью `/ZW` параметра компилятора. Затем можно добавить ссылку на него с помощью **Обозреватель решений**и использовать его в приложениях UWP C++. Свяжите библиотеку DLL с помощью библиотеки экспорта.

Чтобы сделать функциональные возможности доступными вызывающим объектам на других языках, библиотеку можно преобразовать в компонент среды выполнения Windows. Среда выполнения Windows компоненты отличаются от обычных библиотек DLL тем, что они включают в себя метаданные в виде *`.winmd`* файлов, описывающих содержимое способом, необходимым для потребителей .NET и JavaScript.  Чтобы предоставить доступ к элементам API для других языков, можно добавить конструкции C++/CX, такие как ссылочные классы, и сделать их открытыми. В Windows 10 и более поздних версиях вместо C++/CX. рекомендуется использовать [библиотеку c++/WinRT](https://github.com/microsoft/cppwinrt)

Предыдущее обсуждение не относится к COM-компонентам, которые должны обрабатываться по-разному. Если в EXE или DLL имеется сервер COM, его можно использовать в универсальном проекте Windows. Упакуйте его как [COM-компонент без регистрации](/windows/win32/sbscs/creating-registration-free-com-objects), добавьте его в проект как файл содержимого и создайте его экземпляр с помощью [`CoCreateInstanceFromApp`](/windows/win32/api/combaseapi/nf-combaseapi-cocreateinstancefromapp) . Дополнительные сведения см. в статье [Использование DLL без COM в проекте C++ для Магазина Windows](/archive/blogs/win8devsupport/using-free-com-dll-in-windows-store-c-project).

Если вы хотите перенести существующую библиотеку COM в UWP, можно также преобразовать ее в среда выполнения Windows компонент. Для таких портов рекомендуется использовать библиотеку C++/WinRT, но можно также воспользоваться [библиотекой шаблонов c++ среда выполнения Windows (WRL)](../cppcx/wrl/windows-runtime-cpp-template-library-wrl.md). WRL является устаревшим и не поддерживает все функции ATL и OLE. Возможность использования такого порта зависит от возможностей COM, ATL и OLE, необходимых для компонента.

Независимо от того, какие сценарии разработки выбраны, следует иметь в виду несколько определений макросов. Эти макросы можно использовать в коде, чтобы компилировать код условно в классической версии Win32 и UWP.

```cpp
#if WINAPI_FAMILY_PARTITION(WINAPI_PARTITION_PC_APP)
#if WINAPI_FAMILY_PARTITION(WINAPI_PARTITION_PHONE_APP)
#if WINAPI_FAMILY_PARTITION(WINAPI_PARTITION_APP)
#if WINAPI_FAMILY_PARTITION(WINAPI_PARTITION_DESKTOP)
```

Эти операторы могут применяться соответственно к приложениям UWP, приложениям Магазина Windows Phone, к обоим видам приложений или ни к одному из них (то есть, только к классическим приложениям Win32). Эти макросы доступны только в Windows SDK 8,1 и более поздних версиях.

Эта статья содержит следующие процедуры.

- [Использование DLL-библиотеки Win32 в приложении UWP](#BK_Win32DLL)

- [Использование собственной статической библиотеки C++ в приложении UWP](#BK_StaticLib)

- [Перенос библиотеки C++ в компонент среда выполнения Windows](#BK_WinRTComponent)

## <a name="using-a-win32-dll-in-a-uwp-app"></a><a name="BK_Win32DLL"></a> Использование библиотеки DLL Win32 в приложении UWP

Для повышения безопасности и надежности универсальные приложения для Windows работают в среде с ограниченной средой выполнения. Вы не можете использовать любую собственную библиотеку DLL так же, как и классическое приложение для Windows. Исходный код для библиотеки DLL можно перенести для выполнения на платформе UWP. Сначала следует изменить несколько параметров проекта и метаданных файла проекта, чтобы определять проект как проект UWP. Вы перекомпилируете код библиотеки с помощью `/ZW` параметра, который включает C++/CX. Некоторые вызовы API не допускаются в приложениях UWP, так как они связаны с более четкими элементами управления, связанными с этой средой. Дополнительные сведения см. в статье [интерфейсы API Win32 и com для приложений UWP](/uwp/win32-and-com/win32-and-com-for-uwp-apps).

При наличии собственной библиотеки DLL, которая экспортирует функции с помощью `__declspec(dllexport)`, эти функции можно вызывать из приложения UWP путем повторной компиляции библиотеки DLL как проекта UWP. Например, предположим, что у нас есть проект Win32 DLL с именем *Giraffe* , который экспортирует пару классов и их методов с помощью кода, подобного следующему файлу заголовка:

```cpp
// giraffe.h
// Define GIRAFFE_EXPORTS when building this DLL
#pragma once

#ifdef GIRAFFE_EXPORTS
#define GIRAFFE_API __declspec(dllexport)
#else
#define GIRAFFE_API
#endif

GIRAFFE_API int giraffeFunction();

class Giraffe
{
    int id;
        Giraffe(int id_in);
    friend class GiraffeFactory;

public:
    GIRAFFE_API int GetID();
};

class GiraffeFactory
{
    static int nextID;

public:
    GIRAFFE_API GiraffeFactory();
    GIRAFFE_API static int GetNextID();
    GIRAFFE_API static Giraffe* Create();
};
```

И следующий файл кода:

```cpp
// giraffe.cpp
#include "pch.h"
#include "giraffe.h"

Giraffe::Giraffe(int id_in) : id(id_in)
{
}

int Giraffe::GetID()
{
    return id;
}

int GiraffeFactory::nextID = 0;

GiraffeFactory::GiraffeFactory()
{
    nextID = 0;
}

int GiraffeFactory::GetNextID()
{
    return nextID;
}

Giraffe* GiraffeFactory::Create()
{
    return new Giraffe(nextID++);
}

int giraffeFunction();
```

Все остальное в проекте ( *`pch.h`* , *`dllmain.cpp`* ) является частью стандартного шаблона проекта Win32. Код определяет макрос `GIRAFFE_API` , который разрешается в, `__declspec(dllexport)` когда `GIRAFFE_EXPORTS` определен. То есть он определяется при построении проекта в виде библиотеки DLL, но не в том случае, если клиент использует *`giraffe.h`* заголовок. Эту библиотеку DLL можно использовать в проекте UWP, не изменяя исходный код. Необходимо изменить только некоторые параметры и свойства проекта.

Следующая процедура применяется при наличии собственной библиотеки DLL, предоставляющей функции, использующие `__declspec(dllexport)` .

### <a name="to-port-a-native-dll-to-the-uwp-without-creating-a-new-project"></a>Перенос собственной библиотеки DLL на UWP без создания нового проекта

1. Откройте проект DLL в Visual Studio.

1. Откройте **Свойства проекта** библиотеки DLL и задайте **конфигурацию** для **всех конфигураций**.

1. В **свойствах проекта** на вкладке **C/C++** > **Общие** установите значение **Да (/ZW)** для параметра **Использовать расширение среды выполнения Windows**. Это свойство включает расширения компонентов (C++/CX).

1. В **Обозреватель решений**выберите узел проекта, откройте контекстное меню и выберите команду **Выгрузить проект**. Затем откройте контекстное меню узла выгруженного проекта и выберите команду редактирования файла проекта. Найдите элемент `WindowsTargetPlatformVersion` и замените его на следующие элементы.

    ```xml
    <AppContainerApplication>true</AppContainerApplication>
    <ApplicationType>Windows Store</ApplicationType>
    <WindowsTargetPlatformVersion>10.0.10156.0</WindowsTargetPlatformVersion>
    <WindowsTargetPlatformMinVersion>10.0.10156.0</WindowsTargetPlatformMinVersion>
    <ApplicationTypeRevision>10.0</ApplicationTypeRevision>
    ```

   Закройте *`.vcxproj`* файл, снова откройте контекстное меню и выберите **Перезагрузить проект**.

   **Обозреватель решений** теперь определяет проект как универсальный проект Windows.

1. Убедитесь, что файл предкомпилированного заголовка имеет правильное имя. В разделе **предварительно скомпилированные заголовки** может потребоваться изменить **файл предкомпилированного заголовка** с *`pch.h`* на или наоборот, *`stdafx.h`* Если отображается сообщение об ошибке следующего вида:

   > Ошибка C2857: оператор "#include", указанный в **`/Ycpch.h`** параметре командной строки, не найден в исходном файле

   Причина в том, что старые шаблоны проектов используют другое соглашение об именовании для файла предкомпилированного заголовка. В проектах Visual Studio 2019 и более поздних версий используется *`pch.h`* .

1. Выполните построение проекта. Могут возникнуть ошибки, связанные с несовместимыми параметрами командной строки. Например, нерекомендуемый сейчас, но часто используемый ранее параметр **Включить минимальное перестроение (/Gm)** задан по умолчанию во многих старых проектах C++ и не совместим с параметром `/ZW`.

   Некоторые функции недоступны при компиляции для универсальная платформа Windows. Вы увидите ошибки компилятора о проблемах. Устраните эти ошибки, пока не будет выполнена чистая сборка.

1. Чтобы использовать библиотеку DLL в приложении UWP в том же решении, откройте контекстное меню узла проекта UWP и выберите команду **Добавить**  >  **ссылку**.

   В **Projects**разделе  >  **решение**проектов установите флажок рядом с проектом DLL и нажмите кнопку **ОК** .

1. Включите файлы заголовков библиотеки в файл приложения UWP *`pch.h`* .

    ```cpp
    #include "..\Giraffe\giraffe.h"
    ```

1. Обычным способом добавьте код в проекте UWP, чтобы вызывать функции и создавать типы из библиотеки DLL.

    ```cpp
    MainPage::MainPage()
    {
        InitializeComponent();
        GiraffeFactory gf;
        Giraffe* g = gf.Create();
        int id = g->GetID();
    }
    ```

## <a name="using-a-native-c-static-library-in-a-uwp-app"></a><a name="BK_StaticLib"></a> Использование собственной статической библиотеки C++ в приложении UWP

Собственную статическую библиотеку C++ можно использовать в проекте UWP, однако существуют некоторые ограничения, которые необходимо принимать во внимание. Начните с изучения раздела о [статических библиотеках C++/CX](../cppcx/static-libraries-c-cx.md). Доступ к машинному коду в статической библиотеке можно выполнить из приложения UWP, однако в такой библиотеке не рекомендуется создавать открытые ссылочные типы. При компиляции статической библиотеки с параметром `/ZW` библиотекарь (фактически скрытый компоновщик) выводит следующее предупреждение:

> LNK4264: архивирует объектный файл, скомпилированный с параметром /ZW, в статическую библиотеку; обратите внимание, что при создании типов среды выполнения Windows не рекомендуется привязка к статической библиотеке, содержащей метаданные среды выполнения Windows

Однако можно использовать статическую библиотеку в приложении UWP без ее перекомпиляции с помощью `/ZW` . Библиотека не может объявлять ссылочные типы или использовать конструкции C++/CX. Но если ваша цель — просто использовать библиотеку машинного кода, это можно сделать, выполнив следующие действия.

### <a name="to-use-a-native-c-static-library-in-a-uwp-project"></a>Использование собственной статической библиотеки C++ в проекте UWP

1. В свойствах проекта проекта UWP выберите **Свойства конфигурации**  >  **Linker**  >  **входные данные** компоновщика в левой области. В области справа добавьте путь к библиотеке в свойстве **Дополнительные зависимости**. Например, для библиотеки в проекте, в которой размещаются выходные данные *`<SolutionFolder>\Debug\MyNativeLibrary\MyNativeLibrary.lib`* , добавьте относительный путь *`Debug\MyNativeLibrary\MyNativeLibrary.lib`* .

1. Добавьте оператор include для ссылки на файл заголовка в *`pch.h`* файл (если он есть) или в любом файле при *`.cpp`* необходимости и начните добавлять код, использующий библиотеку.

   ```cpp
   #include "..\MyNativeLibrary\MyNativeLibrary.h"
   ```

   Не добавляйте ссылку в узел **References** в **Обозреватель решений**. Этот механизм работает только для компонентов среды выполнения Windows.

## <a name="porting-a-c-library-to-a-windows-runtime-component"></a><a name="BK_WinRTComponent"></a> Перенос библиотеки C++ в компонент среды выполнения Windows

Предположим, что вы хотите использовать собственные API в статической библиотеке из приложения UWP. Если у вас есть исходный код для собственной библиотеки, можно перенести код в среда выполнения Windows компонент. Она больше не является статической библиотекой; вы превратите его в библиотеку DLL, которую можно использовать в любом приложении UWP C++. В этой процедуре описывается создание нового компонента среда выполнения Windows, использующего расширения C++/CX. Сведения о создании компонента, использующего C++/WinRT, см. в разделе [Среда выполнения Windows Components with c++/WinRT](/windows/uwp/winrt-components/create-a-windows-runtime-component-in-cppwinrt).

При использовании C++/CX можно добавлять ссылочные типы и другие конструкции C++/CX, которые доступны клиентам в любом коде приложения UWP. Доступ к этим типам можно получить из C#, Visual Basic или JavaScript. Ниже описываются основные действия.

- Создайте проект компонента среда выполнения Windows (универсальное Windows),
- Скопируйте в него код для статической библиотеки и
- Устраните все ошибки компилятора, вызванные `/ZW` параметром.

### <a name="to-port-a-c-library-to-a-windows-runtime-component"></a>Перенос библиотеки C++ в компонент среды выполнения Windows

1. Создайте проект среда выполнения Windowsного компонента (универсальное Windows).

1. Закройте проект.

1. В **проводнике Windows**Откройте новый проект. Затем найдите проект библиотеки C++, содержащий код, который требуется перенести. Скопируйте исходные файлы (файлы заголовков, файлы кода и другие ресурсы, включая в подкаталогах) из проекта библиотеки C++. Вставьте их в папку нового проекта, убедившись в том, что вы сохранили ту же структуру папок.

1. Повторно откройте проект компонента среда выполнения Windows. Откройте контекстное меню узла проекта в **Обозреватель решений**и выберите пункт **Добавить**  >  **существующий элемент**.

1. Выберите все файлы для добавления из исходного проекта и нажмите кнопку **ОК**. При необходимости повторите эти действия для вложенных папок.

1. На этом этапе может появиться повторяющийся код. Если имеется несколько предварительно скомпилированных заголовков (скажем, *`stdafx.h`* и *`pch.h`* ), выберите один из них для сохранения. В него скопируйте необходимый код, например выражения include. Затем удалите другой, а в свойствах проекта в разделе **предварительно скомпилированные заголовки**убедитесь, что имя файла заголовка указано правильно.

   Если файл был изменен для использования в качестве предкомпилированного заголовка, убедитесь в правильности параметров предкомпилированных заголовков для каждого файла. Последовательно выберите каждый *`.cpp`* файл, откройте его окно свойств и убедитесь, что для параметра все задано значение **использовать (/Yu)**, за исключением предкомпилированного заголовка, который должен быть установлен в значение **создать (/Yc)**.

1. Постройте проект и устраните все ошибки. Эти ошибки могут быть вызваны с помощью `/ZW` параметра или могут быть вызваны новой версией Windows SDK. Кроме того, они могут отражать зависимости, такие как файлы заголовков, от которых зависит ваша библиотека, или отличия параметров проекта от старого проекта к новому.

1. Добавьте в проект общие ссылочные типы или преобразуйте обычные типы в ссылочные типы. Используйте эти типы, чтобы предоставить точки входа в функциональные возможности, которые нужно вызывать из приложений UWP.

1. Протестируйте компонент, добавив ссылку на него из проекта приложения UWP, и добавьте код для вызова созданных открытых API.

## <a name="see-also"></a>См. также раздел

[Перенос на универсальную платформу Windows](../porting/porting-to-the-universal-windows-platform-cpp.md)
