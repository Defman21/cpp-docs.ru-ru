---
title: /FA, /Fa (файл листинга)
description: Справочное руководство по параметру компилятора/FA и/FA Microsoft C++ (файл листинга).
ms.date: 11/21/2020
f1_keywords:
- VC.Project.VCCLWCECompilerTool.AssemblerListingLocation
- VC.Project.VCCLCompilerTool.ConfigureASMListing
- VC.Project.VCCLWCECompilerTool.AssemblerOutput
- VC.Project.VCCLCompilerTool.AssemblerListingLocation
- /fa
- VC.Project.VCCLCompilerTool.AssemblerOutput
- VC.Project.VCCLCompilerTool.UseUnicodeForAssemblerListing
helpviewer_keywords:
- FA compiler option [C++]
- /FA compiler option [C++]
- -FA compiler option [C++]
- listing file type
- assembly-only listing
ms.openlocfilehash: 7e8e39fea55bb69eaa0ae914eeabcafef4ac7849
ms.sourcegitcommit: 432c24dde31c400437c4320e8432b1ddb232f844
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2020
ms.locfileid: "96440231"
---
# <a name="fa-fa-listing-file"></a>`/FA`, `/Fa` (Файл листинга)

Создает файл листинга, содержащий код ассемблера.

## <a name="syntax"></a>Синтаксис

> **`/FA`**[**`c`**\][**`s`**\][**`u`**]\
> **`/Fa`**_контура_

## <a name="remarks"></a>Комментарии

**`/FA`** Параметр компилятора создает файл листинга ассемблера для каждой записи преобразования в компиляции, которая обычно соответствует исходному файлу C или C++. По умолчанию в файл листинга включается только ассемблер, который кодируется как ANSI. Необязательные **`c`** **`s`** аргументы, и **`u`** **`/FA`** используются для управления выводом машинного кода или исходного кода вместе со списком ассемблера, а также сведения о том, кодируется ли список как UTF-8.

По умолчанию каждый файл списка получает то же базовое имя, что и исходный файл, и имеет *`.asm`* расширение. При включении машинного кода с **`c`** параметром файл списка имеет *`.cod`* расширение. Можно изменить имя и расширение файла листинга и каталога, в котором он создается, с помощью **`/Fa`** параметра.

### <a name="fa-arguments"></a>Аргументы `/FA`

None
В список включен только язык ассемблера.

**`c`**\
Необязательный параметр. Включает машинный код в список.

**`s`**\
Необязательный параметр. Включает исходный код в список.

**`u`**\
Необязательный параметр. Кодирует файл листинга в формате UTF-8 и включает метку порядка байтов. По умолчанию файл кодируется как ANSI. Используйте **`u`** для создания файла листинга, который правильно отображается в любой системе, или если в качестве входных данных для компилятора используются файлы исходного кода в Юникоде.

Если **`s`** указаны и **`u`** , и, и если в файле исходного кода используется кодировка Юникод, отличная от UTF-8, то строки кода в *`.asm`* файле могут отображаться неправильно.

### <a name="fa-argument"></a>Аргумент `/Fa`

None
Один *Исходный ASM* -файл создается для каждого файла исходного кода при компиляции.

*файлов*\
Компилятор помещает файл листинга с именем *filename*. ASM в текущий каталог. Эта форма аргумента допустима только при компиляции одного файла исходного кода.

*имя файла. расширение*\
Компилятор помещает файл листинга с именем *filename. extension* в текущий каталог. Эта форма аргумента допустима только при компиляции одного файла исходного кода.

*каталоги*__\\__\
Компилятор создает один файл *source_file. ASM* для каждого файла исходного кода при компиляции. Он помещается в указанный *Каталог*. Обратная косая черта обязательна. Разрешены только пути на текущем диске.

*Каталог* __\\__ *имя файла*\
Файл листинга с именем *filename. ASM* помещается в указанный *Каталог*. Эта форма аргумента допустима только при компиляции одного файла исходного кода.

*Каталог* __\\__ *имя файла. расширение*\
Файл листинга с именем *filename. extension* помещается в указанный *Каталог*. Эта форма аргумента допустима только при компиляции одного файла исходного кода.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите **Configuration Properties**  >  страницу свойств выходные файлы **C/C++** свойства конфигурации  >  **Output Files** .

1. Измените свойство **выходные данные ассемблера** , чтобы задать параметры **/fac** и **/FAS** для ассемблера, компьютера и исходного кода. Измените свойство **использовать Юникод для ассемблерного списка** , чтобы задать **`/FAu`** параметр для выходных данных ANSI или UTF-8. Измените **Расположение списка ASM** , чтобы задать **`/Fa`** параметр для вывода имени и расположения файла.

Установка обоих **выходных данных ассемблера** и **Использование Юникода для свойств листинга ассемблера** может привести к [D9025 предупреждений командной строки](../../error-messages/tool-errors/command-line-warning-d9025.md). Чтобы объединить эти параметры в интегрированной среде разработки, используйте поле **Дополнительные параметры** на странице свойств **командной строки** .

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. описания свойств <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AssemblerListingLocation%2A> и <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AssemblerOutput%2A>. Сведения об указании **/Фау** см. в разделе <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A> .

## <a name="example"></a>Пример

Следующая командная строка создает Объединенный исходный код и листинг машинного кода с именем *`HELLO.cod`* :

```cmd
CL /FAcs HELLO.CPP
```

## <a name="see-also"></a>См. также раздел

[Параметры OUTPUT-File (/F)](output-file-f-options.md)\
[Параметры компилятора КОМПИЛЯТОРОМ MSVC](compiler-options.md)\
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)\
[Указание пути](specifying-the-pathname.md)
