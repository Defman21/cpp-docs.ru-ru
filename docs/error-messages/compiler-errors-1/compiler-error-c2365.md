---
description: 'Дополнительные сведения о: Ошибка компилятора C2365'
title: Ошибка компилятора C2365
ms.date: 11/04/2016
f1_keywords:
- C2365
helpviewer_keywords:
- C2365
ms.assetid: 35839b0b-4055-4b79-8957-b3a0871bdd02
ms.openlocfilehash: e8968e7cc56355c213e88d2e4aeecfb1044e4550
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97210937"
---
# <a name="compiler-error-c2365"></a>Ошибка компилятора C2365

"член класса": переопределение; предыдущим определением было "член класса"

Вы попытались переопределить член класса.

Следующий пример приводит к возникновению ошибки C2365:

```cpp
// C2365.cpp
// compile with: /c
class C1 {
   int CFunc();
   char *CFunc;   // C2365, already exists as a member function

   int CMem;
   char *CMem();   // C2365, already exists as a data member
};
```
