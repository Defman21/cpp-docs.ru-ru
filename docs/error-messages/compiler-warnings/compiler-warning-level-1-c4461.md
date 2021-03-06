---
description: 'Дополнительные сведения: предупреждение компилятора (уровень 1) C4461'
title: Предупреждение компилятора (уровень 1) C4461
ms.date: 11/04/2016
f1_keywords:
- C4461
helpviewer_keywords:
- C4461
ms.assetid: 104ffecc-3dd4-4cb1-89a8-81154fbe46d9
ms.openlocfilehash: 2efb92ca26f9e6cf76f7777c8a50ac657f73554d
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97311010"
---
# <a name="compiler-warning-level-1-c4461"></a>Предупреждение компилятора (уровень 1) C4461

"тип": Этот класс содержит финализатор "финализатор", но не имеет деструктор "dtor"

Наличие метода завершения в типе означает, что ресурсы нужно удалить. Если метод завершения явно не вызывается из деструктора типа, среда CLR определяет, когда следует запускать метод завершения, после того, как объект выходит из области действия.

При определении деструктора в типе и явном вызове метода завершения из деструктора можно детерминированно запускать метод завершения.

Дополнительные сведения см. в разделе [деструкторы и методы завершения](../../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Destructors_and_finalizers).

## <a name="example"></a>Пример

Следующий пример приводит к возникновению ошибки C4461.

```cpp
// C4461.cpp
// compile with: /W1 /clr /c
ref class A {
protected:
   !A() {}   // C4461
};

// OK
ref struct B {
   ~B() {
      B::!B();
   }

   !B() {}
};
```
