---
description: 'Подробнее о следующем: Общие сведения о функциях'
title: Общие сведения о функциях
ms.date: 11/04/2016
helpviewer_keywords:
- functions [C++]
- control flow, function calls
ms.assetid: b6f4637f-02b9-49d8-8601-1f886bd2cfb9
ms.openlocfilehash: b68591d9300cb1a2f63c37c78f4cc03406e9d68f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97243150"
---
# <a name="overview-of-functions"></a>Общие сведения о функциях

Функции должны иметь определение и объявление, хотя определение может служить объявлением, если объявление находится до вызова функции. Определение функции включает тело функции — код, который выполняется при вызове функции.

Объявление функции указывает имя, возвращаемый тип и атрибуты функции, определенной в любом другом месте программы. Объявление функции должно предшествовать вызову функции. Именно поэтому файлы заголовков, содержащие объявления для функций времени выполнения, включаются в код перед вызовом функции времени выполнения. Если объявление содержит сведения о типах и количестве параметров, оно является прототипом. Дополнительные сведения см. в статье [Прототипы функций](../c-language/function-prototypes.md).

Компилятор использует прототип для сравнения типов аргументов в последующих вызовах функции с параметрами функции и для преобразования типов аргументов в типы параметров, если это необходимо.

В вызове функции управление выполнением передается из вызывающей функции в вызываемую функцию. Аргументы, если таковые имеются, передаются по значению в вызываемую функцию. При выполнении оператора **`return`** в вызываемой функции управление и, возможно, значение возвращаются в вызывающую функцию.

## <a name="see-also"></a>См. также

[Функции](../c-language/functions-c.md)
