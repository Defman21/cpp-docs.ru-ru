---
description: 'Дополнительные сведения о: Ошибка компилятора C2061'
title: Ошибка компилятора C2061
ms.date: 11/04/2016
f1_keywords:
- C2061
helpviewer_keywords:
- C2061
ms.assetid: b0e61c0c-a205-4820-b9aa-301d6c6fe6eb
ms.openlocfilehash: e857f4c4de90fadecdd7b7062306391b4222bcf4
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97328728"
---
# <a name="compiler-error-c2061"></a>Ошибка компилятора C2061

Синтаксическая ошибка: идентификатор "идентификатор"

Компилятор обнаружил идентификатор, в котором он не ожидался. Убедитесь, что `identifier` объявлено перед использованием.

Инициализатор может быть заключен в круглые скобки. Чтобы избежать этой проблемы, заключите декларатор в круглые скобки или сделайте его **`typedef`** .

Эта ошибка также может быть вызвана тем, что компилятор обнаруживает выражение как аргумент шаблона класса; Используйте [TypeName](../../cpp/typename.md) , чтобы сообщить компилятору, что он является типом.

Следующий пример приводит к возникновению ошибки C2061:

```cpp
// C2061.cpp
// compile with: /c
template < A a >   // C2061
// try the following line instead
// template < typename b >
class c{};
```

C2061 может возникать, если имя экземпляра передается в [идентификатор typeid](../../extensions/typeid-cpp-component-extensions.md):

```cpp
// C2061b.cpp
// compile with: /clr
ref struct G {
   int i;
};

int main() {
   G ^ pG = gcnew G;
   System::Type ^ pType = typeid<pG>;   // C2061
   System::Type ^ pType2 = typeid<G>;   // OK
}
```
