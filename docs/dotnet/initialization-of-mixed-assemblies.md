---
title: Инициализация смешанных сборок
description: Разработайте с проблемами, которые могут возникнуть во время загрузки и инициализации смешанных сборок.
ms.date: 09/26/2020
helpviewer_keywords:
- mixed assemblies [C++], loader lock
- loader lock [C++]
- initializing mixed assemblies
- deadlocks [C++]
- .cctor [C++]
- custom locales [C++]
- mixed assemblies [C++], initilizing
ms.assetid: bfab7d9e-f323-4404-bcb8-712b15f831eb
ms.openlocfilehash: 6767e6087999138f8e62d3c5a58f972b4e2149ed
ms.sourcegitcommit: 94893973211d0b254c8bcdcf0779997dcc136b0c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2020
ms.locfileid: "91413818"
---
# <a name="initialization-of-mixed-assemblies"></a>Инициализация смешанных сборок

Разработчики Windows всегда должны быть осторожными при блокировке загрузчика во время выполнения кода `DllMain` . Однако при работе с сборками в смешанном режиме C++/CLI необходимо учитывать ряд дополнительных проблем.

Код внутри функции [DllMain](/windows/win32/Dlls/dllmain) не должен иметь доступа к среде CLR .NET. Это означает, что `DllMain` не следует напрямую или косвенно выполнять вызовы управляемых функций; управляемый код не должен быть объявлен или реализован в `DllMain` ; и ни в коем случае не следует выполнять сборку мусора или автоматическую загрузку библиотеки `DllMain` .

## <a name="causes-of-loader-lock"></a>Причины блокировки загрузчика

С появлением платформы .NET можно использовать два разных механизма загрузки модуля выполнения (EXE или DLL): один для Windows, который используется для неуправляемых модулей и один для CLR, который загружает сборки .NET. Проблема загрузки смешанных библиотек DLL касается загрузчика ОС Microsoft Windows.

Когда в процесс загружается сборка, содержащая только конструкции .NET, загрузчик CLR может выполнять все необходимые задачи загрузки и инициализации. Однако для загрузки смешанных сборок, которые могут содержать машинный код и данные, необходимо также использовать загрузчик Windows.

Загрузчик Windows гарантирует, что ни один код не сможет получить доступ к коду или данным в этой библиотеке DLL до инициализации. И это гарантирует, что код не сможет избыточно загрузить библиотеку DLL, пока она не будет частично инициализирована. Для этого загрузчик Windows использует критически важный раздел процесса (часто называемый "блокировкой загрузчика"), который предотвращает ненадежный доступ во время инициализации модуля. В результате процесс загрузки является уязвимым для многих случаев взаимоблокировки. Для смешанных сборок следующие две ситуации повышают риск взаимоблокировки.

- Во-первых, если пользователи пытаются выполнить функции, скомпилированные на языке MSIL, когда блокировка загрузчика удерживается ( `DllMain` например, из или в статических инициализаторах), это может привести к взаимоблокировке. Рассмотрим случай, когда функция MSIL ссылается на тип в сборке, которая еще не загружена. Среда CLR пытается автоматически загрузить эту сборку, а для этого может потребоваться установить блокировку загрузчика Windows. Происходит взаимоблокировка, так как блокировка загрузчика уже удерживается кодом ранее в последовательности вызовов. Однако выполнение кода MSIL во время блокировки загрузчика не гарантирует, что произойдет взаимоблокировка. Именно поэтому этот сценарий трудно диагностировать и исправить. В некоторых случаях, например, если библиотека DLL ссылочного типа не содержит машинных конструкций и все ее зависимости не содержат машинных конструкций, загрузчику Windows не требуется загружать сборку .NET типа, на который указывает ссылка. Кроме того, требуемая сборка или ее зависимые смешанные неуправляемые модули или модули .NET могли быть загружены другим кодом. Следовательно, взаимоблокировку трудно прогнозировать и вероятность ее возникновения зависит от конфигурации целевого компьютера.

- Во-вторых, при загрузке библиотек DLL в версиях 1,0 и 1,1 .NET Framework среда CLR предполагала, что блокировка загрузчика не удерживается, и выполняла несколько действий, недопустимых при блокировке загрузчика. Предполагая, что блокировка загрузчика не удерживается, является допустимым предположением для чисто DLL-библиотек .NET. Но поскольку смешанные библиотеки DLL выполняют собственные процедуры инициализации, они нуждаются в собственном загрузчике Windows и, следовательно, блок загрузчика. Таким образом, даже если разработчик не пытался выполнить какие-либо функции MSIL во время инициализации библиотеки DLL, существовала небольшая вероятность недетерминированной взаимоблокировки в .NET Framework версий 1,0 и 1,1.

Все недетерминированные ситуации при загрузке смешанных библиотек DLL исключены. Это было выполнено с помощью следующих изменений:

- Среда CLR больше не делает ложных предположений при загрузке смешанных DLL.

- Неуправляемая и управляемая инициализация выполняется на двух отдельных этапах. Неуправляемая инициализация выполняется сначала (через `DllMain` ), а управляемая инициализация выполняется через. Поддерживаемая .NET `.cctor` конструкция. Последний полностью прозрачен для пользователя, если не **`/Zl`** **`/NODEFAULTLIB`** используется или. Дополнительные сведения см. в разделе[ `/NODEFAULTLIB` (игнорировать библиотеки)](../build/reference/nodefaultlib-ignore-libraries.md) и [ `/Zl` (не указывайте имя библиотеки по умолчанию)](../build/reference/zl-omit-default-library-name.md).

Блокировка загрузчика все равно может произойти, но теперь эти случаи можно воспроизвести и обнаружить. Если `DllMain` содержит инструкции MSIL, компилятор создает предупреждение о предупреждении [компилятора (уровень 1) C4747](../error-messages/compiler-warnings/compiler-warning-level-1-c4747.md). Кроме того, либо библиотека CRT, либо среда CLR попытаются определить случаи выполнения функций MSIL во время блокировки загрузчика и сообщат о них, если такие были. Если библиотека CRT обнаруживает попытку, выдается ошибка во время выполнения C R6033

В оставшейся части этой статьи описываются оставшиеся сценарии, в которых код MSIL может выполняться при блокировке загрузчика. В нем показано, как устранить проблему в каждом из этих сценариев и методы отладки.

## <a name="scenarios-and-workarounds"></a>Ситуации и способы решения проблем

Существует несколько ситуаций, в которых пользовательский код может выполнять функции MSIL во время блокировки загрузчика. Разработчик должен убедиться, что реализация пользовательского кода не пытается выполнить инструкции MSIL в каждом из этих случаев. В следующих подразделах описываются все возможные ситуации, а также способы решения распространенных проблем.

### <a name="dllmain"></a>DllMain

`DllMain`Функция является определяемой пользователем точкой входа для библиотеки DLL. Если пользователь не указывает иное, функция `DllMain` вызывается каждый раз, когда процесс или поток присоединяется к библиотеке DLL или отсоединяется от нее. Поскольку подобный вызов может произойти во время блокировки загрузчика, запрещается компилировать пользовательские функции `DllMain` в код MSIL. Кроме того, в MSIL нельзя скомпилировать никакую функцию в дереве вызовов с корнем `DllMain` . Чтобы устранить проблемы здесь, блок кода, который определяет, `DllMain` должен быть изменен с помощью `#pragma unmanaged` . То же необходимо сделать для каждой функции, которая вызывается в `DllMain` .

В случаях, когда эти функции должны вызывать функцию, для которой требуется реализация MSIL для других вызывающих контекстов, можно использовать стратегию дублирования, где создаются как .NET, так и собственная версия одной и той же функции.

В качестве альтернативы, если `DllMain` это не требуется или его не нужно выполнять при блокировке загрузчика, можно удалить предоставляемую пользователем `DllMain` реализацию, которая устраняет проблему.

Если `DllMain` пытается выполнить инструкцию MSIL напрямую, будет получено [Предупреждение компилятора (уровень 1) C4747](../error-messages/compiler-warnings/compiler-warning-level-1-c4747.md) . Однако компилятор не может обнаружить случаи, когда `DllMain` вызывает функцию в другом модуле, который, в свою очередь, пытается выполнить код MSIL.

Дополнительные сведения об этом сценарии см. [в статье препятствия для диагностики](#impediments-to-diagnosis).

### <a name="initializing-static-objects"></a>Инициализация статических объектов

Инициализация статических объектов может вызвать взаимоблокировку, если требуется динамический инициализатор. В простых случаях (например, при назначении значения, известного во время компиляции в статическую переменную) не требуется динамическая инициализация, поэтому риск взаимоблокировки отсутствует. Однако некоторые статические переменные инициализируются вызовами функций, вызовами конструкторов или выражениями, которые не могут быть вычислены во время компиляции. Всем этим переменным требуется выполнение кода во время инициализации модуля.

В коде, приведенном ниже, показаны примеры статических инициализаторов, для которых требуется динамическая инициализация: вызов функции, конструирование объекта и инициализация указателя. (Эти примеры не являются статическими, но предполагается, что они имеют определения в глобальной области видимости, что оказывает тот же результат.)

```cpp
// dynamic initializer function generated
int a = init();
CObject o(arg1, arg2);
CObject* op = new CObject(arg1, arg2);
```

Этот риск взаимоблокировки зависит от того, компилируется ли содержащий модуль с **`/clr`** и будет ли выполняться MSIL. В частности, если статическая переменная компилируется без **`/clr`** (или находится в `#pragma unmanaged` блоке), а динамический инициализатор, необходимый для его инициализации, приводит к выполнению инструкций MSIL, может возникнуть взаимоблокировка. Это обусловлено тем, что для модулей, компилируемых без **`/clr`** , Инициализация статических переменных выполняется с помощью DllMain. Напротив, статические переменные, скомпилированные с помощью **`/clr`** , инициализируются с помощью `.cctor` , после завершения неуправляемого этапа инициализации и снятия блокировки загрузчика.

Существует ряд решений о взаимоблокировке, вызванных динамической инициализацией статических переменных. Они расположены примерно в порядке времени, необходимого для устранения проблемы.

- Исходный файл, содержащий статическую переменную, можно скомпилировать с помощью **`/clr`** .

- Все функции, вызываемые статической переменной, могут быть скомпилированы в машинный код с помощью `#pragma unmanaged` директивы.

- Можно вручную клонируйте код, от которого зависит статическая переменная, создав версию .NET и неуправляемую версию с разными именами. Разработчики могут затем вызвать собственную версию из неуправляемых статических инициализаторов и вызывать версию .NET в других случаях.

### <a name="user-supplied-functions-affecting-startup"></a>Пользовательские функции, влияющие на автозагрузку

Существует несколько пользовательских функций, от которых зависит инициализация библиотек при автозагрузке. Например, при глобальном перегрузке операторов в C++, таких как **`new`** операторы и **`delete`** , предоставляемые пользователем версии используются везде, включая инициализацию и уничтожение стандартной библиотеки C++. В результате Стандартная библиотека C++ и статические инициализаторы, предоставляемые пользователем, будут вызывать любые предоставляемые пользователем версии этих операторов.

Если они скомпилированы в код MSIL, эти инициализаторы пытаются выполнить инструкции MSIL во время блокировки загрузчика. Предоставленные пользователем `malloc` данные имеют те же последствия. Чтобы устранить эту проблему, любая из этих перегрузок или определений, предоставляемых пользователем, должна быть реализована в виде машинного кода с помощью `#pragma unmanaged` директивы.

Дополнительные сведения об этом сценарии см. [в статье препятствия для диагностики](#impediments-to-diagnosis).

### <a name="custom-locales"></a>Пользовательские языковые стандарты

Если пользователь предоставляет пользовательский глобальный языковой стандарт, этот языковой стандарт используется для инициализации всех будущих потоков ввода-вывода, включая статически инициализированные потоки. Если объект глобального языкового стандарта скомпилирован в код MSIL, функции элемента этого объекта, скомпилированные в MSIL, могут быть вызваны во время блокировки загрузчика.

Существует три способа решения этой проблемы.

Исходные файлы, содержащие все глобальные определения потоков ввода-вывода, можно скомпилировать с помощью **`/clr`** параметра. Он предотвращает выполнение статических инициализаторов при блокировке загрузчика.

Пользовательские определения функций языкового стандарта можно скомпилировать в машинный код с помощью `#pragma unmanaged` директивы.

Рекомендуется устанавливать пользовательский языковой стандарт как глобальный языковой стандарт только после отключения блокировки загрузчика. Затем следует явно настроить потоки ввода-вывода, созданные во время инициализации с использованием пользовательского языкового стандарта.

## <a name="impediments-to-diagnosis"></a>Трудности при диагностике

В некоторых случаях трудно обнаружить источник взаимоблокировок. В следующих подразделах описываются эти случаи и способы решения возникающих проблем.

### <a name="implementation-in-headers"></a>Реализация в заголовках

В некоторых случаях реализация функций в файлах заголовка может затруднить диагностику. Для встроенных функций и кода шаблона требуется, чтобы функции были заданы в файле заголовка.  Язык C++ указывает "правило одного определения", которое говорит о том, что все реализации функций с одинаковым именем должны быть семантически эквивалентны. Как следствие, компоновщику C++ не требуются особые предосторожности при слиянии объектных файлов с дублированными реализациями определенной функции.

В версиях Visual Studio до Visual Studio 2005 компоновщик просто выбирает самый крупный из этих семантических эквивалентных определений. Это делается для поддержки прямых объявлений и сценариев, когда для различных исходных файлов используются различные параметры оптимизации. Она создает проблему для смешанных библиотек DLL для машинного кода и .NET.

Так как один и тот же заголовок может быть включен в файлы C++ с **`/clr`** включенным и отключенным, или #include можно обернуть внутри `#pragma unmanaged` блока, возможно наличие как MSIL, так и собственных версий функций, предоставляющих реализации в заголовках. В реализациях MSIL и Native для инициализации при блокировке загрузчика существует разная семантика, которая фактически нарушает правило одного определения. Следовательно, когда компоновщик выбирает самую значительную реализацию, он может выбрать версию MSIL функции, даже если она была явно скомпилирована в машинный код в других местах с помощью `#pragma unmanaged` директивы. Чтобы гарантировать, что версия MSIL шаблона или встроенной функции никогда не вызывается при блокировке загрузчика, каждое определение каждой такой функции, вызываемой в рамках блокировки загрузчика, должно быть изменено с помощью `#pragma unmanaged` директивы. Если файл заголовка отличается от третьей стороны, самым простым способом внесения этого изменения является принудительная отправка директивы по директиве `#pragma unmanaged` #include для файла заголовков, вызывающих проблемы. (Пример см. в разделе [управляемые, неуправляемые](../preprocessor/managed-unmanaged.md) .) Однако эта стратегия не работает для заголовков, содержащих другой код, который должен напрямую вызывать API-интерфейсы .NET.

Для удобства пользователей, решающих проблему блокировку загрузчика, компоновщик выбирает реализацию на машинном, а не управляемом коде, если существует две версии реализации. Это значение по умолчанию позволяет избежать описанных выше проблем. Однако в этом выпуске существует два исключения этого правила из-за двух неразрешенных проблем с компилятором:

- Вызов встроенной функции осуществляется через указатель глобальной статической функции. Этот сценарий недоступен, так как виртуальные функции вызываются с помощью указателей на глобальные функции. Например,

```cpp
#include "definesmyObject.h"
#include "definesclassC.h"

typedef void (*function_pointer_t)();

function_pointer_t myObject_p = &myObject;

#pragma unmanaged
void DuringLoaderlock(C & c)
{
    // Either of these calls could resolve to a managed implementation,
    // at link-time, even if a native implementation also exists.
    c.VirtualMember();
    myObject_p();
}
```

### <a name="diagnosing-in-debug-mode"></a>Диагностика в режиме отладки

Вся диагностика проблем блокировки загрузчика должна проходить в отладочных построениях. Сборки выпуска могут не создавать диагностику. Кроме того, оптимизация, выполненная в режиме выпуска, может маскировать некоторые из сценариев MSIL в сценариях блокировки загрузчика.

## <a name="how-to-debug-loader-lock-issues"></a>Отладка проблем с блокировкой загрузчика

Диагностика, которую создает среда CLR при вызове функции MSIL, приводит к тому, что CLR приостанавливает выполнение. Это, в свою очередь, приводит к приостановке Visual C++ отладчика смешанного режима при запуске отлаживаемого процесса. Однако при присоединении к процессу ит'сн'т возможность получения управляемого стека вызовов для отлаживаемого кода с помощью смешанного отладчика.

Чтобы определить конкретную функцию MSIL, вызванную во время блокировки загрузчика, разработчики должны выполнить следующие действия.

1. Убедитесь, что доступны символы для библиотек mscoree.dll и mscorwks.dll.

   Символы можно сделать доступными двумя способами. Первый способ заключается в том, что PDB-файлы для библиотек mscoree.dll и mscorwks.dll можно добавить к пути поиска. Чтобы добавить их, откройте диалоговое окно Параметры пути поиска символов. (В меню **Сервис** выберите пункт **Параметры**. В левой области диалогового окна **Параметры** откройте узел **Отладка** и выберите **символы**.) Добавьте путь к файлам mscoree.dll и mscorwks.dll PDB-файлы в список поиска. Эти файлы устанавливаются в каталог % VSINSTALLDIR%\SDK\v2.0\symbols. Нажмите кнопку **ОК**.

   Второй способ заключается в том, что PDB-файлы для mscoree.dll и mscorwks.dll можно загрузить с сервера символов Майкрософт. Для настройки сервера символов откройте диалоговое окно параметров пути поиска символов. (В меню **Сервис** выберите пункт **Параметры**. В левой области диалогового окна **Параметры** откройте узел **Отладка** и выберите **символы**.) Добавьте следующий путь поиска в список поиска: `https://msdl.microsoft.com/download/symbols` . Добавьте каталог кэша символов в текстовом поле кэша сервера символов. Нажмите кнопку **ОК**.

1. Для отладчика установите режим отладки только машинного кода.

   Откройте сетку **Свойства** для запускаемого проекта в решении. Выберите **Свойства конфигурации** > **Отладка**. Задайте для свойства **Тип отладчика** значение **только машинный код**.

1. Запустите отладчик (F5).

1. После **`/clr`** создания диагностики выберите **повторить** и нажмите кнопку **прервать**.

1. Откройте окно "Стек вызовов". (В строке меню выберите **Отладка**  >  . **Windows**  >  **Стек вызовов**.) Вызывающий ошибку `DllMain` или статический инициализатор обозначается зеленой стрелкой. Если функция, вызвавшая ошибку, не определена, необходимо выполнить следующие действия, чтобы найти ее.

1. Откройте окно **Интерпретация** (в строке меню выберите **Отладка**  >  **Windows**  >  **немедленного**запуска Windows).

1. Войдите в `.load sos.dll` окно **интерпретации** , чтобы загрузить службу отладки SOS.

1. `!dumpstack`Чтобы получить полный список внутреннего стека, введите в окно **Immediate** **`/clr`** .

1. Найдите первый экземпляр (ближайший к концу стека) любого _CorDllMain (если `DllMain` вызывается ошибка) или _VTableBootstrapThunkInitHelperStub или жеттаржетфорвтаблинтри (если статический инициализатор вызывает ошибку). Запись в стеке сразу под этим вызовом является вызовом функции, реализованной в коде MSIL, которая была вызвана во время блокировки загрузчика.

1. Перейдите к исходному файлу и номеру строки, указанным на предыдущем шаге, и устраните проблему с помощью сценариев и решений, описанных в разделе сценарии.

## <a name="example"></a>Пример

### <a name="description"></a>Описание

В следующем примере показано, как избежать блокировки загрузчика путем перемещения кода из `DllMain` в конструктор глобального объекта.

В этом примере имеется глобальный управляемый объект, конструктор которого содержит управляемый объект, изначально находился в `DllMain` . Вторая часть этого примера ссылается на сборку, создавая экземпляр управляемого объекта для вызова конструктора модуля, который выполняет инициализацию.

### <a name="code"></a>Код

```cpp
// initializing_mixed_assemblies.cpp
// compile with: /clr /LD
#pragma once
#include <stdio.h>
#include <windows.h>
struct __declspec(dllexport) A {
   A() {
      System::Console::WriteLine("Module ctor initializing based on global instance of class.\n");
   }

   void Test() {
      printf_s("Test called so linker doesn't throw away unused object.\n");
   }
};

#pragma unmanaged
// Global instance of object
A obj;

extern "C"
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved) {
   // Remove all managed code from here and put it in constructor of A.
   return true;
}
```

В этом примере демонстрируются проблемы при инициализации смешанных сборок:

```cpp
// initializing_mixed_assemblies_2.cpp
// compile with: /clr initializing_mixed_assemblies.lib
#include <windows.h>
using namespace System;
#include <stdio.h>
#using "initializing_mixed_assemblies.dll"
struct __declspec(dllimport) A {
   void Test();
};

int main() {
   A obj;
   obj.Test();
}
```

Этот код выводит следующие результаты:

```Output
Module ctor initializing based on global instance of class.

Test called so linker doesn't throw away unused object.
```

## <a name="see-also"></a>См. также раздел

[Смешанные (собственные и управляемые) сборки](../dotnet/mixed-native-and-managed-assemblies.md)
