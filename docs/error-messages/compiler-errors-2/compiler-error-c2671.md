---
description: 'Дополнительные сведения о: Ошибка компилятора C2671'
title: Ошибка компилятора C2671
ms.date: 11/04/2016
f1_keywords:
- C2671
helpviewer_keywords:
- C2671
ms.assetid: fc0ee40f-c8f3-408f-b89d-745d149c4169
ms.openlocfilehash: ec70961a9ea57920a56f2b460a5e6ed481963233
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97282111"
---
# <a name="compiler-error-c2671"></a>Ошибка компилятора C2671

"функция": статические функции члена не имеют указателей "this"

**`static`** Функция-член попыталась получить доступ **`this`** .

Следующий пример приводит к возникновению ошибки C2671:

```cpp
// C2671.cpp
struct S {
   static S* const func() { return this; }  // C2671
};
```
