---
description: 'Дополнительные сведения о: Ошибка компилятора C2283'
title: Ошибка компилятора C2283
ms.date: 11/04/2016
f1_keywords:
- C2283
helpviewer_keywords:
- C2283
ms.assetid: 8a5b3175-b480-4598-a1f7-0b50504c5caa
ms.openlocfilehash: dab8688623962051759f9f4be84f5831b58a700f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97294981"
---
# <a name="compiler-error-c2283"></a>Ошибка компилятора C2283

"идентификатор": чистый спецификатор или абстрактный спецификатор переопределения не допускаются в безымянной структуре

Функция-член неименованного класса или структуры объявляется с чистым спецификатором, что не допускается.

В следующем примере возникает ошибка C2283:

```cpp
// C2283.cpp
// compile with: /c
struct {
   virtual void func() = 0;   // C2283
};
struct T {
   virtual void func() = 0;   // OK
};
```
