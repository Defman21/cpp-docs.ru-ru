---
description: 'Дополнительные сведения о: Ошибка компилятора C2655'
title: Ошибка компилятора C2655
ms.date: 11/04/2016
f1_keywords:
- C2655
helpviewer_keywords:
- C2655
ms.assetid: beaefa6e-51b3-4df9-9150-960f3fbf40e0
ms.openlocfilehash: 113de213ab53892447666824c48510f7c9654d4e
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97286115"
---
# <a name="compiler-error-c2655"></a>Ошибка компилятора C2655

"идентификатор": определение или повторное объявление недопустимо в текущей области видимости

Идентификатор может быть повторно объявлен только в глобальной области видимости.

Следующий пример приводит к возникновению ошибки C2655:

```cpp
// C2655.cpp
class A {};
class B {
public:
   static int i;
};

int B::i;  // OK

int main() {
   A B::i;  // C2655
}
```
