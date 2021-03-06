---
description: 'Дополнительные сведения о: Ошибка компилятора C2171'
title: Ошибка компилятора C2171
ms.date: 11/04/2016
f1_keywords:
- C2171
helpviewer_keywords:
- C2171
ms.assetid: a80343b5-ab3f-4413-b6f1-3ce9d7e519e5
ms.openlocfilehash: 8e2749d3af9a7fafa38b1f1bdcb99874e45f4531
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97322241"
---
# <a name="compiler-error-c2171"></a>Ошибка компилятора C2171

"оператор": недопустимо для операндов типа "тип"

Унарный оператор используется с недопустимым типом операнда.

## <a name="examples"></a>Примеры

Следующий пример приводит к возникновению ошибки C2171:

```cpp
// C2171.cpp
int main() {
   double d, d1;
   d = ~d1;   // C2171

   // OK
   int d2 = 0, d3 = 0;
   d2 = ~d3;
}
```

Следующий пример приводит к возникновению ошибки C2171:

```cpp
// C2171_b.cpp
// compile with: /c
class A {
public:
   A() { STF( &A::D ); }

   void D() {}
   void DTF() {
      (*TF)();   // C2171
      (this->*TF)();   // OK
   }

   void STF(void (A::*fnc)()) {
      TF = fnc;
   }

private:
   void (A::*TF)();
};
```
