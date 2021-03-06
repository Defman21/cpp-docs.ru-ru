---
description: Дополнительные сведения см. в статье как обнаруживать компиляцию/CLR.
title: Пошаговое руководство. обнаружение и компиляция CLR
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- compilation, detecting /clr
- /clr compiler option [C++], detecting use of
ms.assetid: a9310045-4810-4637-a64a-0b31a08791c1
ms.openlocfilehash: 25cd241a08f79bcae629c05fb3c7982a387120ce
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97175720"
---
# <a name="how-to-detect-clr-compilation"></a>Практическое руководство. Определение факта использования ключа /clr при компиляции

Используйте `_MANAGED` макрос или, `_M_CEE` чтобы проверить, компилируется ли модуль с **параметром/CLR**. Дополнительные сведения см. в разделе [/CLR (компиляция среды CLR)](../build/reference/clr-common-language-runtime-compilation.md).

Дополнительные сведения о макросах см. в разделе [предопределенные макросы](../preprocessor/predefined-macros.md).

## <a name="example"></a>Пример

```cpp
// detect_CLR_compilation.cpp
// compile with: /clr
#include <stdio.h>

int main() {
   #if (_MANAGED == 1) || (_M_CEE == 1)
      printf_s("compiling with /clr\n");
   #else
      printf_s("compiling without /clr\n");
   #endif
}
```

## <a name="see-also"></a>См. также раздел

[Использование взаимодействия C++ (неявный PInvoke)](../dotnet/using-cpp-interop-implicit-pinvoke.md)
