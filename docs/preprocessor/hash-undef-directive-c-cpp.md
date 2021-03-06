---
description: 'Дополнительные сведения о директиве: #undef (C/C++)'
title: '#Директива undef (C/C++)'
ms.date: 08/29/2019
f1_keywords:
- '#undef'
helpviewer_keywords:
- '#undef directive'
- undef directive (#undef)
- preprocessor, directives
ms.assetid: 88900e0e-2c19-4a63-b681-f3d3133c24ca
ms.openlocfilehash: 20dfd1d0b26f18a26e7ad407704d6cb0ffd563bb
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97300442"
---
# <a name="undef-directive-cc"></a>Директива #undef (C/C++)

Удаляет имя, ранее созданное с помощью `#define`, то есть отменяет его определение.

## <a name="syntax"></a>Синтаксис

>  *идентификатор* #undef

## <a name="remarks"></a>Комментарии

Директива **#undef** удаляет текущее определение *идентификатора*. Следовательно, последующие вхождения *идентификатора* игнорируются препроцессором. Чтобы удалить определение макроса с помощью **#undef**, укажите только *идентификатор* макроса, а не список параметров.

Можно также применить директиву **#undef** к идентификатору, не имеющему предыдущего определения. Это гарантирует, что идентификатор не определен. Замена макросов не выполняется в инструкциях **#undef** .

Директива **#undef** обычно сопряжена с `#define` директивой для создания области в исходной программе, в которой идентификатор имеет специальное значение. Например, определенная функция программы-источника может использовать константы манифестов для определения значений среды, которые не влияют на остальные части программы. Директива **#undef** также работает с `#if` директивой для управления условной компиляцией исходной программы. Дополнительные сведения см. [в разделе директивы #if, #elif, #else и #endif](../preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp.md).

В следующем примере директива **#undef** удаляет определения символьной константы и макроса. Обратите внимание, что предоставляется только идентификатор макроса.

```C
#define WIDTH 80
#define ADD( X, Y ) ((X) + (Y))
.
.
.
#undef WIDTH
#undef ADD
```

**Блок, относящийся только к системам Microsoft**

Макросы могут быть неопределенными из командной строки с помощью `/U` параметра, за которым следуют имена макросов, которые должны быть неопределенными. Результат выполнения этой команды эквивалентен последовательности `#undef` операторов *имени макроса* в начале файла.

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[Директивы препроцессора](../preprocessor/preprocessor-directives.md)
