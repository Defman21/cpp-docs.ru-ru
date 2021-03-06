---
description: 'Дополнительные сведения о: Ошибка компилятора C2743'
title: Ошибка компилятора C2743
ms.date: 11/04/2016
f1_keywords:
- C2743
helpviewer_keywords:
- C2743
ms.assetid: 644cd444-21d2-471d-a176-f5f52c5a0b73
ms.openlocfilehash: 2619d4a0dd2b89d36f11944b59c2ab4993d95fd0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97123062"
---
# <a name="compiler-error-c2743"></a>Ошибка компилятора C2743

"тип": невозможно перехватывать собственный тип с деструктором __clrcall или конструктором копии

Модуль, скомпилированный с помощью **параметра/clr** , попытался перехватить исключение собственного типа, где деструктор типа или конструктор копий использует `__clrcall` соглашение о вызовах.

При компиляции с **параметром/CLR** обработка исключений ждет, что функции-члены в собственном типе будут [__cdecl](../../cpp/cdecl.md) , а не [__clrcall](../../cpp/clrcall.md). Собственные типы с функциями-членами с использованием `__clrcall` соглашения о вызовах не могут быть перехвачены в модуле, скомпилированном с **параметром/CLR**.

Дополнительные сведения см. в разделе [/CLR (компиляция среды CLR)](../../build/reference/clr-common-language-runtime-compilation.md).

## <a name="example"></a>Пример

Следующий пример приводит к возникновению ошибки C2743.

```cpp
// C2743.cpp
// compile with: /clr
public struct S {
   __clrcall ~S() {}
};

public struct T {
   ~T() {}
};

int main() {
   try {}
   catch(S) {}   // C2743
   // try the following line instead
   // catch(T) {}

   try {}
   catch(S*) {}   // OK
}
```
