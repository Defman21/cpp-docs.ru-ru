---
description: 'Дополнительные сведения о: Ошибка компилятора C2164'
title: Ошибка компилятора C2164
ms.date: 11/04/2016
f1_keywords:
- C2164
helpviewer_keywords:
- C2164
ms.assetid: 55df5024-68a8-45a8-ae6c-e6dba35318a2
ms.openlocfilehash: 9afe0809075f83c77ffae2ef77bc72c9e0f194e7
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97145524"
---
# <a name="compiler-error-c2164"></a>Ошибка компилятора C2164

"функция": подставляемая функция не объявлена

`intrinsic`Директива pragma использует необъявленную функцию (возникает только с **/Oi**). Или одна из встроенных функций компилятора была использована без включения файла заголовка.

Следующий пример приводит к возникновению ошибки C2164:

```c
// C2164.c
// compile with: /c
// processor: x86
// Uncomment the following line to resolve.
// #include "xmmintrin.h"
void b(float *p) {
   _mm_load_ss(p);   // C2164
}
```
