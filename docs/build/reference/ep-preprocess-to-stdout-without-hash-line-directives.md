---
description: 'Дополнительные сведения о:/EP (Предварительная обработка в stdout без директив #line)'
title: '/EP (предварительная обработка в поток стандартных выходных файлов без директив #line)'
ms.date: 11/04/2016
f1_keywords:
- /ep
- VC.Project.VCCLCompilerTool.GeneratePreprocessedFileNoLines
helpviewer_keywords:
- copy preprocessor output to stdout
- preprocessor output, copy to stdout
- -EP compiler option [C++]
- EP compiler option [C++]
- /EP compiler option [C++]
ms.assetid: 6ec411ae-e33d-4ef5-956e-0054635eabea
ms.openlocfilehash: cbd36cd6bdafe315a7a6ef01b46857725033bd69
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97201005"
---
# <a name="ep-preprocess-to-stdout-without-line-directives"></a>/EP (предварительная обработка в поток стандартных выходных файлов без директив #line)

Предварительно обрабатывает исходные файлы C и C++ и копирует предварительно обработанные файлы на стандартное выходное устройство.

## <a name="syntax"></a>Синтаксис

```
/EP
```

## <a name="remarks"></a>Remarks

В процессе выполняются все директивы препроцессора, выполняются расширения макросов и удаляются комментарии. Чтобы сохранить комментарии в предварительно обработанном выводе, используйте параметр [/c (сохранять комментарии во время предварительной обработки)](c-preserve-comments-during-preprocessing.md) с помощью параметра **/EP**.

Параметр **/EP** подавляет компиляцию. Необходимо повторно отправить предварительно обработанный файл для компиляции. **/EP** также подавляет вывод выходных файлов из параметров **/FA**, **/FA** и **/FM** . Дополнительные сведения см. в разделе [/FA,/FA (файл листинга)](fa-fa-listing-file.md) и параметр [/FM (имя файла сопоставления)](fm-name-mapfile.md).

Ошибки, созданные на последующих этапах обработки, ссылаются на номера строк предварительно обработанного файла, а не на исходный файл. Если необходимо, чтобы номера строк ссылались на исходный исходный файл, используйте параметр [/e (Предварительная обработка в stdout)](e-preprocess-to-stdout.md) . Параметр **/e** добавляет `#line` директивы в выходные данные для этой цели.

Чтобы отправить предварительно обработанные выходные данные с `#line` директивами в файл, используйте параметр [/p (Предварительная обработка в файл)](p-preprocess-to-a-file.md) .

Для отправки предварительно обработанных выходных данных в stdout с `#line` директивами используйте параметр **/P** и **/EP** вместе.

Нельзя использовать предкомпилированные заголовки с параметром **/EP** .

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Откройте папку **C/C++** .

1. Щелкните страницу свойств **препроцессора** .

1. Измените свойство **создать предварительно обработанный файл** .

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.GeneratePreprocessedFile%2A>.

## <a name="example"></a>Пример

Следующая командная строка выполняет предварительную обработку файла `ADD.C` , сохраняет комментарии и отображает результат на стандартном устройстве вывода:

```
CL /EP /C ADD.C
```

## <a name="see-also"></a>См. также раздел

[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)
