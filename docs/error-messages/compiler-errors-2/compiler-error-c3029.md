---
description: 'Дополнительные сведения о: Ошибка компилятора C3029'
title: Ошибка компилятора C3029
ms.date: 11/04/2016
f1_keywords:
- C3029
helpviewer_keywords:
- C3029
ms.assetid: 655eb04d-504a-468d-8c0c-bda1e5f297b7
ms.openlocfilehash: ec9164c43dd44e4fe69273c2cad7c3e6beead394
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97174186"
---
# <a name="compiler-error-c3029"></a>Ошибка компилятора C3029

"символ": может появиться только один раз в предложениях совместного использования данных в директиве OpenMP

Символ использовался больше одного раза в одном или нескольких предложениях директивы. Символ можно использовать только один раз в директиве.

При компиляции следующего примера возникнет ошибка C3029:

```cpp
// C3029.cpp
// compile with: /openmp /link vcomps.lib
#include "omp.h"

int g_i;

int main() {
   int i, x;

   #pragma omp parallel reduction(+ : x, x)   // C3029
      ;

   #pragma omp parallel reduction(+ : x)   // OK
      ;

   #pragma omp parallel private(x) reduction(+ : x)   // C3029
      ;

   #pragma omp parallel reduction(+ : x)   // OK
      ;
}
```
