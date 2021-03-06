---
description: Дополнительные сведения о:/MIDL (указание параметров командной строки MIDL)
title: /MIDL (Указание параметров командной строки MIDL)
ms.date: 09/05/2018
f1_keywords:
- /midl
- VC.Project.VCLinkerTool.MidlCommandFile
helpviewer_keywords:
- -MIDL linker option
- MIDL
- /MIDL linker option
- MIDL linker option
- MIDL, command line options
ms.assetid: 22dc259e-b34c-4ed3-a380-4beb734482c1
ms.openlocfilehash: 7c3a095e687ebe58db25cc8313569df3ee3a5886
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97190644"
---
# <a name="midl-specify-midl-command-line-options"></a>/MIDL (Указание параметров командной строки MIDL)

Указывает файл ответов для параметров командной строки MIDL

## <a name="syntax"></a>Синтаксис

> **/MIDL: \@** <em>файл</em>

## <a name="arguments"></a>Аргументы

*файл*<br/>
Имя файла, содержащего [Параметры командной строки MIDL](/windows/win32/Midl/general-midl-command-line-syntax).

## <a name="remarks"></a>Комментарии

Все параметры для преобразования IDL-файла в файл TLB должны быть заданы в *файле*. Параметры командной строки MIDL нельзя указывать в командной строке компоновщика. Если/MIDL не указан, компилятор MIDL будет вызываться только с именем IDL-файла и без других параметров.

Файл должен содержать один параметр командной строки MIDL для каждой строки.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Задание данного параметра компоновщика в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите   >  страницу свойств  >  **встроенного IDL** -свойства компоновщика свойства конфигурации.

1. Измените свойство **команды MIDL** .

### <a name="to-set-this-linker-option-programmatically"></a>Задание данного параметра компоновщика программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.MidlCommandFile%2A>.

## <a name="see-also"></a>См. также раздел

[Справочник по компоновщику MSVC](linking.md)<br/>
[Параметры компоновщика MSVC](linker-options.md)<br/>
[/IDLOUT (имя выходных файлов MIDL)](idlout-name-midl-output-files.md)<br/>
[/IGNOREIDL (не обрабатывать атрибуты в MIDL)](ignoreidl-don-t-process-attributes-into-midl.md)<br/>
[/TLBOUT (имя. TLB-файл)](tlbout-name-dot-tlb-file.md)<br/>
[Сборка атрибутированной программы](../../windows/attributes/cpp-attributes-com-net.md)
