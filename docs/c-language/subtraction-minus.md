---
description: 'Подробнее о следующем: Вычитание (-)'
title: Вычитание (-)
ms.date: 11/04/2016
helpviewer_keywords:
- operators [C], subtraction
- subtraction operator, syntax
ms.assetid: 9cacba7d-20b3-4372-8a63-ba5d8ee64177
ms.openlocfilehash: 8e0daf4e1bfdbb844df99e3f79dc2baf5a30e6e4
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97114563"
---
# <a name="subtraction--"></a>Вычитание (-)

Оператор вычитания ( **-** ) вычитает второй операнд из первого. Оба операнда могут быть целочисленными типами или типами с плавающей запятой либо один операнд может быть указателем, а второй — целым числом.

При вычитании двух указателей разница преобразуется в целочисленное значение со знаком путем деления разницы на размер значения типа, к которому обращаются указатели. Размер целочисленного значения определяется типом **ptrdiff_t** в стандартном включаемом файле STDDEF.H. Результат представляет собой число позиций памяти данного типа, расположенных между двумя адресами. Результат гарантировано имеет значение только для двух элементов одного массива, как описано в разделе [Арифметические операции с указателями](../c-language/pointer-arithmetic.md).

Если целочисленное значение вычитается из значения указателя, оператор вычитания преобразует целочисленное значение (*i*) путем его умножения на размер значения, к которому обращается указатель. После преобразования значение целого числа представляет позиции памяти *i*, где каждая позиция имеет длину, заданную типом указателя. Если преобразованное целочисленное значение вычесть из значения указателя, будут получены позиции *i* адреса памяти, расположенные до исходного адреса. Новый указатель указывает на значение типа, к которому обращается исходное значение указателя.

## <a name="see-also"></a>См. также

[Аддитивные операторы в C](../c-language/c-additive-operators.md)
