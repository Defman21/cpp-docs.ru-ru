---
description: 'Дополнительные сведения о: Ошибка компилятора C3204'
title: Ошибка компилятора C3204
ms.date: 11/04/2016
f1_keywords:
- C3204
helpviewer_keywords:
- C3204
ms.assetid: 06e578da-0262-48c8-b2ae-be1cd6d28884
ms.openlocfilehash: 8e9275cada58988c9dac3942569fb0416ddff0ba
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97285738"
---
# <a name="compiler-error-c3204"></a>Ошибка компилятора C3204

нельзя вызвать "_alloca" в пределах блока catch

Эта ошибка возникает при использовании вызова [_alloca](../../c-runtime-library/reference/alloca.md) из блока catch.

## <a name="example"></a>Пример

Следующий пример приводит к возникновению ошибки C3204:

```cpp
// C3204.cpp
// compile with: /EHsc
#include <malloc.h>

void ShowError(void)
{
   try
   {
   }
   catch(...)
   {
      _alloca(1);   // C3204
   }
}
```
