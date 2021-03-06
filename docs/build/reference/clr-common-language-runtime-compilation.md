---
title: /clr (компиляция среды CLR)
description: Используйте параметр/CLR компилятора Microsoft C++ для компиляции кода C++/CLI и C++ в качестве управляемого кода.
ms.date: 10/27/2020
f1_keywords:
- /CLR
- VC.Project.VCNMakeTool.CompileAsManaged
- VC.Project.VCCLCompilerTool.CompileAsManaged
helpviewer_keywords:
- cl.exe compiler, common language runtime option
- -clr compiler option [C++]
- clr compiler option [C++]
- /clr compiler option [C++]
- Managed Extensions for C++, compiling
- common language runtime, /clr compiler option
ms.assetid: fec5a8c0-40ec-484c-a213-8dec918c1d6c
ms.openlocfilehash: 9d27d9fb6226f84c4ea67a8f9387a595ba65468b
ms.sourcegitcommit: 9c801a43ee0d4d84956b03fd387716c818705e0d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907601"
---
# <a name="clr-common-language-runtime-compilation"></a>`/clr` (Компиляция среды CLR)

Позволяет приложениям и компонентам использовать функции среды CLR и выполнять компиляцию C++/CLI.

## <a name="syntax"></a>Синтаксис

> **`/clr`**\[**`:`**_Параметры_ ]

## <a name="arguments"></a>Аргументы

*Параметры*\
Один или несколько из следующих аргументов с разделителями-запятыми.

- нет

   При отсутствии параметров **`/clr`** создает метаданные для компонента. Метаданные могут использоваться другими приложениями CLR и позволяют компоненту использовать типы и данные в метаданных других компонентов среды CLR. Дополнительные сведения см. в статье [Смешанные (собственные и управляемые) сборки](../../dotnet/mixed-native-and-managed-assemblies.md).

- **`NetCore`**

   **`/clr:NetCore`** Создает метаданные и код для компонента с помощью последней кросс-платформенной платформы .NET Framework, также известной как .NET Core. Метаданные могут использоваться другими приложениями .NET Core. Кроме того, параметр позволяет компоненту использовать типы и данные в метаданных других компонентов .NET Core.

- **`nostdlib`**

   Указывает компилятору игнорировать каталог по умолчанию *`\clr`* . Компилятор выдает ошибки при включении нескольких версий библиотеки DLL, например System.dll. Этот параметр позволяет указать конкретную платформу для использования во время компиляции.

- **`pure`**

   **`/clr:pure` не рекомендуется к использованию** . Этот параметр удален в Visual Studio 2017 и более поздних версий. Мы рекомендуем перенести код, который должен быть чистым кодом MSIL, на C#.

- **`safe`**

   **`/clr:safe` не рекомендуется к использованию** . Этот параметр удален в Visual Studio 2017 и более поздних версий. Мы рекомендуем перенести код, который должен быть безопасным кодом MSIL, на C#.

- **`noAssembly`**

   **`/clr:noAssembly` не рекомендуется к использованию** . Вместо этого используйте [ `/LN` (создать модуль MSIL)](ln-create-msil-module.md) .

   Указывает компилятору не вставлять манифест сборки в выходной файл. По умолчанию **`noAssembly`** параметр не действует.

   Управляемая программа, не имеющая метаданных сборки в манифесте, называется *модулем* . **`noAssembly`** Параметр можно использовать только для создания модуля. Если компиляция выполняется с помощью [`/c`](c-compile-without-linking.md) и **`/clr:noAssembly`** , то [`/NOASSEMBLY`](noassembly-create-a-msil-module.md) для создания модуля необходимо указать параметр на этапе компоновщика.

   До выхода Visual Studio 2005 **`/clr:noAssembly`** обязательно **`/LD`** . **`/LD`** Теперь подразумевается при указании **`/clr:noAssembly`** .

- **`initialAppDomain`**

   **`initialAppDomain` является устаревшим** . Позволяет запускать приложение C++/CLI в среде CLR версии 1.  Приложение, компилируемое с помощью, **`initialAppDomain`** не должно использоваться приложением, использующим ASP.NET, так как оно не поддерживается в версии 1 среды CLR.

## <a name="remarks"></a>Remarks

*Управляемый код* — это код, который может проверяться и УПРАВЛЯТЬся средой CLR. Управляемый код может обращаться к управляемым объектам. Дополнительные сведения см. в разделе [ `/clr` ограничения](clr-restrictions.md).

Сведения о разработке приложений, которые определяют и потребляют управляемые типы в C++, см. в разделе [расширения компонентов для платформ среды выполнения](../../extensions/component-extensions-for-runtime-platforms.md).

Приложение, скомпилированное с использованием, **`/clr`** может не содержать управляемые данные.

Сведения о включении отладки в управляемом приложении см. в разделе [ `/ASSEMBLYDEBUG` (Add DebuggableAttribute)](assemblydebug-add-debuggableattribute.md).

В куче с сбором мусора создаются экземпляры только типов CLR. Дополнительные сведения см. в статье [Классы и структуры](../../extensions/classes-and-structs-cpp-component-extensions.md). Для компиляции функции в машинный код используйте директиву `unmanaged` pragma. Дополнительные сведения см. [ `managed` в разделе `unmanaged` , ](../../preprocessor/managed-unmanaged.md).

По умолчанию **`/clr`** не действует. Если **`/clr`** действует, действует **`/MD`** также и. Дополнительные сведения см. [ `/MD` в разделе `/MT` , `/LD` (использование библиотеки Run-Time)](md-mt-ld-use-run-time-library.md). **`/MD`** гарантирует, что в стандартных файлах заголовков выбираются динамически связываемые многопоточные версии подпрограмм среды выполнения. Многопоточность необходима для управляемого программирования, так как сборщик мусора CLR запускает методы завершения во вспомогательном потоке.

При компиляции с помощью служб **`/c`** можно указать тип CLR выходного файла с помощью [`/CLRIMAGETYPE`](clrimagetype-specify-type-of-clr-image.md) параметра компоновщика.

**`/clr`** подразумевает **`/EHa`** , что другие **`/EH`** параметры для не поддерживаются **`/clr`** . Дополнительные сведения см. в разделе [ `/EH` (модель обработки исключений)](eh-exception-handling-model.md).

Сведения о том, как определить тип образа среды CLR для файла, см. в разделе [`/CLRHEADER`](clrheader.md) .

Все модули, передаваемые в данный вызов компоновщика, должны быть скомпилированы с помощью одного и того же параметра компилятора библиотеки времени выполнения ( **`/MD`** или **`/LD`** ).

Используйте [`/ASSEMBLYRESOURCE`](assemblyresource-embed-a-managed-resource.md) параметр компоновщика для внедрения ресурса в сборку. [`/DELAYSIGN`](delaysign-partially-sign-an-assembly.md)[`/KEYCONTAINER`](keycontainer-specify-a-key-container-to-sign-an-assembly.md) [`/KEYFILE`](keyfile-specify-key-or-key-pair-to-sign-an-assembly.md) Параметры компоновщика, и позволяют настроить способ создания сборки.

Если **`/clr`** используется, `_MANAGED` символ определяется как 1. Дополнительные сведения см. в разделе [стандартные макросы](../../preprocessor/predefined-macros.md).

Глобальные переменные в собственном объектном файле инициализируются первыми ( `DllMain` Если исполняемый файл является библиотекой DLL), а затем инициализируются глобальные переменные в управляемом разделе (перед запуском любого управляемого кода). [`#pragma init_seg`](../../preprocessor/init-seg.md) влияет только на порядок инициализации в управляемых и неуправляемых категориях.

### <a name="metadata-and-unnamed-classes"></a>Метаданные и неименованные классы

Неименованные классы отображаются в метаданных под именами, например  `$UnnamedClass$<crc-of-current-file-name>$<index>$` , где `<index>` — это последовательный счетчик неименованных классов в компиляции. Например, следующий код создает неименованный класс в метаданных.

```cpp
// clr_unnamed_class.cpp
// compile by using: /clr /LD
class {} x;
```

Для просмотра метаданных используйте ildasm.exe.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Задайте для раскрывающегося списка **Конфигурация** значение **все конфигурации** и задайте для раскрывающегося списка **платформа** значение **все платформы** .

1. Выберите страницу **Свойства конфигурации**  >  **C/C++**  >  **Общие** .

1. Измените свойство **Поддержка среды CLR** . Выберите **ОК** для сохранения внесенных изменений.

> [!NOTE]
> В интегрированной среде разработки Visual Studio **`/clr`** параметр компилятора можно задать по отдельности на странице Общие **Свойства конфигурации**  >  **C/C++** в  >  **General** диалоговом окне страницы свойств. Однако мы рекомендуем использовать шаблон CLR для создания проекта. Он задает все свойства, необходимые для успешного создания компонента среды CLR. Другим способом установки этих свойств является использование свойства **Поддержка среды CLR** на странице **Свойства конфигурации**  >  **Дополнительно** диалогового окна страницы свойств. Это свойство задает одновременно все прочие параметры средств, связанных со средой CLR.

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.CompileAsManaged>.

## <a name="see-also"></a>См. также

[Параметры компилятора КОМПИЛЯТОРОМ MSVC](compiler-options.md)\
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)
