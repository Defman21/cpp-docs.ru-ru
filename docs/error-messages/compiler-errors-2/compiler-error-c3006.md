---
description: 'Дополнительные сведения о: Ошибка компилятора C3006'
title: Ошибка компилятора C3006
ms.date: 11/04/2016
f1_keywords:
- C3006
helpviewer_keywords:
- C3006
ms.assetid: 449082ec-fd45-4c47-8ab3-ba6a719e4dc4
ms.openlocfilehash: e2c6372b86f7677f3beeaed5335798f10e01c82e
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97274558"
---
# <a name="compiler-error-c3006"></a>Ошибка компилятора C3006

"предложение": в предложении директивы OpenMP "директива" отсутствует необходимый аргумент

В директиве OpenMP отсутствует ожидаемый аргумент.

Следующий пример приводит к возникновению ошибки C3006:

```c
// C3006.c
// compile with: /openmp
int main()
{
   #pragma omp parallel shared   // C3006
   // Try the following line instead:
   // #pragma omp parallel shared(x) {}

}
```
