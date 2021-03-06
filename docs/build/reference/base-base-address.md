---
description: Дополнительные сведения о:/BASE (базовый адрес)
title: /BASE (базовый адрес)
ms.date: 09/05/2018
f1_keywords:
- /base
- VC.Project.VCLinkerTool.BaseAddress
helpviewer_keywords:
- base addresses [C++]
- programs [C++], preventing relocation
- semicolon [C++], specifier
- -BASE linker option
- key address size
- environment variables [C++], LIB
- programs [C++], base address
- LIB environment variable
- BASE linker option
- DLLs [C++], linking
- /BASE linker option
- '@ symbol for base address'
- executable files [C++], base address
- at sign symbol for base address
ms.assetid: 00b9f6fe-0bd2-4772-a69c-7365eb199069
ms.openlocfilehash: 269911c7d9fce47be1b9755ddebf38170ea4e81c
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97182779"
---
# <a name="base-base-address"></a>/BASE (базовый адрес)

Указывает базовый адрес программы.

## <a name="syntax"></a>Синтаксис

> **/Base:**{*адрес*[**,**<em>Размер</em>] | **\@** <em>имя файла</em>**,**<em>ключ</em>}

## <a name="remarks"></a>Комментарии

> [!NOTE]
> По соображениям безопасности корпорация Майкрософт рекомендует использовать параметр [/DynamicBase](dynamicbase-use-address-space-layout-randomization.md) вместо указания базовых адресов для исполняемых файлов. При этом создается исполняемый образ, который может быть случайным образом переопределяться во время загрузки с помощью функции выбора макета адресного пространства (ASLR) Windows. Параметр/DYNAMICBASE по умолчанию включен.

Параметр/BASE задает базовый адрес программы, переопределяя расположение по умолчанию для exe-или DLL-файла. Базовый адрес для EXE-файла по умолчанию — 0x400000 для 32-разрядных изображений или 0x140000000 для 64-разрядных изображений. Для библиотеки DLL базовый адрес по умолчанию — 0x10000000 для 32-разрядных изображений или 0x180000000 для 64-разрядных изображений. В операционных системах, которые не поддерживают случайный выбор структуры адресного пространства (ASLR) или если не задан параметр/DYNAMICBASE: NO, операционная система сначала пытается загрузить программу по указанному или базовому адресу по умолчанию. Если в нем достаточно места, система перемещает программу. Чтобы предотвратить перемещение, используйте параметр [/fixed](fixed-fixed-base-address.md) .

Компоновщик выдает ошибку, если *адрес* не кратен 64 КБ. При необходимости можно указать размер программы; компоновщик выдает предупреждение, если программа не умещается в указанном размере.

В командной строке другим способом указания базового адреса является использование файла ответов базового адреса. Файл ответов базового адреса — это текстовый файл, содержащий базовые адреса и дополнительные размеры всех библиотек DLL, которые будут использоваться программой, и уникальный текстовый ключ для каждого базового адреса. Чтобы указать базовый адрес с помощью файла ответов, используйте символ at ( **\@** ), за которым следует имя файла ответов, *имя* файла и запятая, а затем значение *ключа* для базового адреса, используемого в файле. Компоновщик ищет *имя файла* по указанному пути или значение, если путь не указан, в каталогах, указанных в переменной среды LIB. Каждая строка в файле *filename* представляет одну библиотеку DLL и имеет следующий синтаксис:

>  *адрес* ключа [*Размер*] **;** *Комментарий*

*Ключ* представляет собой строку из буквенно-цифровых символов и не учитывает регистр. Обычно это имя библиотеки DLL, но это не обязательно. За *ключом* следует базовый *адрес* в формате C-Language, шестнадцатеричной или десятичной нотации, а также необязательный максимальный *Размер*. Все три аргумента разделяются пробелами или символами табуляции. Компоновщик выдает предупреждение, если указанный *Размер* меньше, чем виртуальное адресное пространство, требуемое для программы. *Комментарий* задается точкой с запятой (**;**) и может находиться в той же или отдельной строке. Компоновщик игнорирует весь текст от точки с запятой до конца строки. В этом примере показана часть такого файла:

```
main   0x00010000    0x08000000    ; for PROJECT.exe
one    0x28000000    0x00100000    ; for DLLONE.DLL
two    0x28100000    0x00300000    ; for DLLTWO.DLL
```

Если файл, содержащий эти строки, называется DLLS.txt, приведенный ниже пример команды применяют эти сведения.

```
link dlltwo.obj /dll /base:@dlls.txt,two
```

Другой способ задать базовый адрес — использовать *базовый* аргумент в инструкции [Name](name-c-cpp.md) или [Library](library.md) . Параметры/BASE и [/DLL](dll-build-a-dll.md) эквивалентны оператору **Library** .

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Задание данного параметра компоновщика в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите вкладку **Свойства конфигурации**  >  **компоновщика**  >  **Дополнительные** свойства.

1. Измените свойство **базового адреса** .

### <a name="to-set-this-linker-option-programmatically"></a>Задание данного параметра компоновщика программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.BaseAddress%2A>.

## <a name="see-also"></a>См. также раздел

[Справочник по компоновщику MSVC](linking.md)<br/>
[Параметры компоновщика MSVC](linker-options.md)
