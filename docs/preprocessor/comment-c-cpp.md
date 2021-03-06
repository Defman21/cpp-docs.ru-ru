---
description: 'Дополнительные сведения: Комментарий pragma'
title: comment - прагма
ms.date: 08/29/2019
f1_keywords:
- vc-pragma.comment
- comment_CPP
helpviewer_keywords:
- annotations [C++]
- comments [C++], compiled files
- pragmas, comment
- comment pragma
ms.assetid: 20f099ff-6303-49b3-9c03-a94b6aa69b85
ms.openlocfilehash: 71172632ee1589c3f6d66136e9567929bff5d08c
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97300818"
---
# <a name="comment-pragma"></a>comment - прагма

Вставляет запись комментария в объектный или исполняемый файл.

## <a name="syntax"></a>Синтаксис

> **#pragma комментарий (** *Комментарий-Type* [ **,** "*Комментарий-Строка*"] **)**

## <a name="remarks"></a>Комментарии

*Тип Comment* — это один из стандартных идентификаторов, описанных ниже, который указывает тип записи комментария. Необязательный *Комментарий-String* — это строковый литерал, предоставляющий дополнительные сведения для некоторых типов комментариев. Так как *Комментарий-Строка* является строковым литералом, он подчиняется всем правилам для строковых литералов по отношению к экранированным символам, внедренным кавычкам ( `"` ) и объединению.

### <a name="compiler"></a>compiler

Задает в объектном файле имя и номер версии компилятора. Эта запись комментария игнорируется компоновщиком. Если для этого типа записей указан параметр *строки Comment* , компилятор выдает предупреждение.

### <a name="lib"></a>lib

Задает в объектном файле запись поиска библиотеки. Этот тип комментария должен сопровождаться параметром *строки Comment* , содержащим имя (и, возможно, путь) библиотеки, которую должен искать компоновщик. Имя библиотеки соответствует библиотеке по умолчанию — поиску записей в объектном файле; Компоновщик ищет эту библиотеку так же, как если бы она была названа в командной строке, при условии, что библиотека не указана с параметром [/NODEFAULTLIB](../build/reference/nodefaultlib-ignore-libraries.md). В один и тот же исходный файл можно вставить несколько записей поиска библиотеки. В объектном файле они будут располагаться в том же порядке, что и в исходном.

Если важен порядок использования библиотеки по умолчанию и добавленной библиотеки, при компиляции с параметром [/Zl](../build/reference/zl-omit-default-library-name.md) имя библиотеки по умолчанию не будет помещено в модуль объекта. Далее можно вставить еще одну директиву #pragma comment и с ее помощью добавить имя библиотеки по умолчанию уже после добавленной библиотеки. Библиотеки, добавленные при помощи этих директив, будут находиться в объектном модуле в том же порядке, в каком они указаны в исходном коде.

### <a name="linker"></a>компоновщик

Помещает [параметр компоновщика](../build/reference/linker-options.md) в объектный файл. Благодаря этому параметр компоновщика можно не передавать из командной строки и не указывать в среде разработки, а задать непосредственно в комментарии. Например, в нем можно задать параметр /include, чтобы принудительно включить символ:

```C
#pragma comment(linker, "/include:__mySymbol")
```

Для передачи в идентификатор компоновщика доступны только следующие параметры компоновщика (*comment-Type*):

- [/DEFAULTLIB](../build/reference/defaultlib-specify-default-library.md)

- [/EXPORT](../build/reference/export-exports-a-function.md)

- [/INCLUDE](../build/reference/include-force-symbol-references.md)

- [/MANIFESTDEPENDENCY](../build/reference/manifestdependency-specify-manifest-dependencies.md)

- [/MERGE](../build/reference/merge-combine-sections.md)

- [/SECTION](../build/reference/section-specify-section-attributes.md)

### <a name="user"></a>пользователь

Вставляет в объектный файл комментарий общего рода. Параметр *строки Comment* содержит текст комментария. Эта запись комментария игнорируется компоновщиком.

## <a name="examples"></a>Примеры

Следующая директива pragma указывает компоновщику найти библиотеку EMAPI.LIB во время компоновки. Сначала компоновщик ищет ее в текущем рабочем каталоге, а затем по пути, заданном в переменной среды LIB.

```C
#pragma comment( lib, "emapi" )
```

Следующая директива pragma указывает компилятору вставить в объектный файл имя и номер версии компилятора:

```C
#pragma comment( compiler )
```

Для комментариев, которые принимают параметр *строки комментария* , можно использовать макрос в любом месте, где используется строковый литерал, при условии, что макрос разворачивается до строкового литерала. Кроме того, можно указать конкатенацию любого набора строковых литералов и макросов, которые развертываются в строковые литералы. Допустимым примером является следующая инструкция:

```C
#pragma comment( user, "Compiled on " __DATE__ " at " __TIME__ )
```

## <a name="see-also"></a>См. также раздел

[Директивы pragma и ключевое слово __pragma](../preprocessor/pragma-directives-and-the-pragma-keyword.md)
