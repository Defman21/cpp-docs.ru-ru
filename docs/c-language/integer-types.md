---
description: 'Подробнее о следующем: Целочисленные типы'
title: Целочисленные типы
ms.date: 07/22/2020
helpviewer_keywords:
- integer data type, integer types in C++
- integer constants
- integer types
- integers, types
ms.assetid: c8926a5e-0e98-4e37-9b05-ce97961379bd
ms.openlocfilehash: 0142a6c9394851bc65df0150db40eb2228dd0fe3
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97181843"
---
# <a name="integer-types"></a>Целочисленные типы

Всем целым константам присваивается тип на основе их значения и способа представления. Для любой целой константы можно принудительно задать тип **`long`** , добавив букву **`l`** или **`L`** в конец константы; для принудительного задания типа **`unsigned`** добавьте в конец значения букву **`u`** или **`U`** . Следует избегать использования буквы **`l`** в нижнем регистре, так как ее можно перепутать с цифрой 1. Ниже приведены некоторые формы целых констант **`long`** :

```C
/* Long decimal constants */
10L
79L

/* Long octal constants */
012L
0115L

/* Long hexadecimal constants */
0xaL or 0xAL
0X4fL or 0x4FL

/* Unsigned long decimal constant */
776745UL
778866LU
```

Тип, присваиваемый константе, зависит от значения, которое она представляет. Значение константы должно находиться в диапазоне представимых значений для ее типа. Тип константы определяет, какие преобразования выполняются при использовании константы в выражении или при добавлении знака "минус" ( **`-`** ). В этом списке перечислены правила преобразования целых констант.

- Для десятичной константы без суффикса используется тип **`int`** , **`long int`** или **`unsigned long int`** . Константе присваивается первый из этих 3 типов, в котором возможно представление значения константы.

- Восьмеричным или шестнадцатеричным константам без суффиксов присваивается тип **`int`** , **`unsigned int`** , **`long int`** или **`unsigned long int`** в зависимости от размера константы.

- Константам с суффиксом **`u`** или **`U`** присваивается тип **`unsigned int`** или **`unsigned long int`** в зависимости от размера.

- Константам с суффиксом **`l`** или **`L`** присваивается тип **`long int`** или **`unsigned long int`** в зависимости от размера.

- Константам с суффиксом **`u`** или **`U`** и **`l`** или **`L`** присваивается тип **`unsigned long int`** .

## <a name="see-also"></a>См. также

[Целочисленные константы в C](../c-language/c-integer-constants.md)
