---
description: 'Дополнительные сведения: предупреждение компилятора (уровень 4) C4233'
title: Предупреждение компилятора (уровень 4) C4233
ms.date: 10/25/2017
f1_keywords:
- C4233
helpviewer_keywords:
- C4233
ms.assetid: 9aa51fc6-8ef3-43b5-bafb-c9333cf60de3
ms.openlocfilehash: 3e797bcefeaeee615014ea8e0bd109e4cf4ffbef
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97344020"
---
# <a name="compiler-warning-level-4-c4233"></a>Предупреждение компилятора (уровень 4) C4233

> использовано нестандартное расширение: ключевое слово "*keyword*" поддерживается только в C++, а не в C

Компилятор компилирует исходный код как C, а не C++, и вы использовали ключевое слово, допустимое только в C++. Компилятор компилирует исходный файл как C, если файл исходного кода имеет расширение. C или используется параметр [/TC](../../build/reference/tc-tp-tc-tp-specify-source-file-type.md).

Это предупреждение автоматически повышается до ошибки. Если вы хотите изменить это поведение, используйте [#pragma предупреждение](../../preprocessor/warning.md). Например, чтобы сделать C4233 проблемой с предупреждением уровня 4, добавьте следующую строку в файл исходного кода:

```cpp
#pragma warning(4:4233)
```
