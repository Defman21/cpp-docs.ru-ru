---
description: 'Подробнее о следующем: Оценка токенов'
title: Оценка токенов
ms.date: 11/04/2016
helpviewer_keywords:
- tokens, evaluating
ms.assetid: 28870b62-dff6-4644-8b75-d58f340b48d2
ms.openlocfilehash: e22a904956b3f429585c6627a7fb2e8f8da6d222
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97196533"
---
# <a name="evaluation-of-tokens"></a>Оценка токенов

Когда компилятор интерпретирует токены, он включает в один токен максимально возможное количество символов, а затем переходит к следующему. Поэтому если токены не разделены пробельными символами, они могут интерпретироваться не так, как ожидается. Рассмотрим следующее выражение:

```
i+++j
```

В этом примере компилятор сначала извлекает максимально возможный оператор (`++`) из последовательности знаков "плюс", а затем обрабатывает последний знак "плюс" как оператор сложения (`+`). Таким образом, выражение интерпретируется как `(i++) + (j)`, а не как `(i) + (++j)`. Для того чтобы предотвратить неоднозначность и гарантировать правильное вычисление выражений, в подобных случаях рекомендуется использовать пробелы и скобки.

**Блок, относящийся только к системам Microsoft**

Компилятор C обрабатывает символ CTRL+Z как индикатор конца файла. Весь текст, расположенный после символа CTRL+Z, игнорируется.

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[Токены C](../c-language/c-tokens.md)
