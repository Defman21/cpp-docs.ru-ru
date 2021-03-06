---
description: Дополнительные сведения о том, как маршалировать структуры с помощью взаимодействия C++.
title: Практическое руководство. Маршалирование структур с помощью взаимодействия C++
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- C++ Interop, structures
- structures [C++], marshaling
- data marshaling [C++], structures
- interop [C++], structures
- marshaling [C++], structures
ms.assetid: c2080200-f983-4d6e-a557-cd870f060a54
ms.openlocfilehash: 96622c48034ddf3126e68867ad5a4bd8ab25fa43
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97302547"
---
# <a name="how-to-marshal-structures-using-c-interop"></a>Практическое руководство. Маршалирование структур с помощью взаимодействия C++

В этом разделе демонстрируется один аспект взаимодействия Visual C++. Дополнительные сведения см. [в разделе Использование взаимодействия C++ (неявный PInvoke)](../dotnet/using-cpp-interop-implicit-pinvoke.md).

В следующих примерах кода используются [управляемые, неуправляемые](../preprocessor/managed-unmanaged.md) директивы #pragma для реализации управляемых и неуправляемых функций в одном и том же файле, но эти функции взаимодействуют одинаково, если они определены в отдельных файлах. Файлы, содержащие только неуправляемые функции, не должны компилироваться с [параметром/CLR (компиляция CLR)](../build/reference/clr-common-language-runtime-compilation.md).

## <a name="example-pass-structure-from-managed-to-unmanaged-function"></a>Пример. Передача структуры из управляемой функции в неуправляемую

В следующем примере показана передача структуры из управляемой в неуправляемую функцию как по значению, так и по ссылке. Так как структура в этом примере содержит только простые встроенные типы данных (см. раздел непреобразуемые и преобразуемые [типы](/dotnet/framework/interop/blittable-and-non-blittable-types)), Специальная упаковка не требуется. Сведения о маршалинге непреобразуемых структур, например, содержащих указатели, см. [в разделе инструкции. маршалирование внедренных указателей с использованием взаимодействия C++](../dotnet/how-to-marshal-embedded-pointers-using-cpp-interop.md).

```cpp
// PassStruct1.cpp
// compile with: /clr

#include <stdio.h>
#include <math.h>

using namespace System;
using namespace System::Runtime::InteropServices;

#pragma unmanaged

struct Location {
   int x;
   int y;
};

double GetDistance(Location loc1, Location loc2) {
   printf_s("[unmanaged] loc1(%d,%d)", loc1.x, loc1.y);
   printf_s(" loc2(%d,%d)\n", loc2.x, loc2.y);

   double h = loc1.x - loc2.x;
   double v = loc1.y = loc2.y;
   double dist = sqrt( pow(h,2) + pow(v,2) );

   return dist;
}

void InitLocation(Location* lp) {
   printf_s("[unmanaged] Initializing location...\n");
   lp->x = 50;
   lp->y = 50;
}

#pragma managed

int main() {
   Location loc1;
   loc1.x = 0;
   loc1.y = 0;

   Location loc2;
   loc2.x = 100;
   loc2.y = 100;

   double dist = GetDistance(loc1, loc2);
   Console::WriteLine("[managed] distance = {0}", dist);

   Location loc3;
   InitLocation(&loc3);
   Console::WriteLine("[managed] x={0} y={1}", loc3.x, loc3.y);
}
```

## <a name="example-pass-structure-from-unmanaged-to-managed-function"></a>Пример. Передача структуры из неуправляемой в управляемую функцию

В следующем примере показана передача структуры из неуправляемой в управляемую функцию как по значению, так и по ссылке. Поскольку структура в этом примере содержит только простые встроенные типы данных (см. раздел непреобразуемые и преобразуемые [типы](/dotnet/framework/interop/blittable-and-non-blittable-types)), особый маршалинг не требуется. Сведения о маршалинге непреобразуемых структур, например, содержащих указатели, см. [в разделе инструкции. маршалирование внедренных указателей с использованием взаимодействия C++](../dotnet/how-to-marshal-embedded-pointers-using-cpp-interop.md).

```cpp
// PassStruct2.cpp
// compile with: /clr
#include <stdio.h>
#include <math.h>
using namespace System;

// native structure definition
struct Location {
   int x;
   int y;
};

#pragma managed

double GetDistance(Location loc1, Location loc2) {
   Console::Write("[managed] got loc1({0},{1})", loc1.x, loc1.y);
   Console::WriteLine(" loc2({0},{1})", loc2.x, loc2.y);

   double h = loc1.x - loc2.x;
   double v = loc1.y = loc2.y;
   double dist = sqrt( pow(h,2) + pow(v,2) );

   return dist;
}

void InitLocation(Location* lp) {
   Console::WriteLine("[managed] Initializing location...");
   lp->x = 50;
   lp->y = 50;
}

#pragma unmanaged

int UnmanagedFunc() {
   Location loc1;
   loc1.x = 0;
   loc1.y = 0;

   Location loc2;
   loc2.x = 100;
   loc2.y = 100;

   printf_s("(unmanaged) loc1=(%d,%d)", loc1.x, loc1.y);
   printf_s(" loc2=(%d,%d)\n", loc2.x, loc2.y);

   double dist = GetDistance(loc1, loc2);
   printf_s("[unmanaged] distance = %f\n", dist);

   Location loc3;
   InitLocation(&loc3);
   printf_s("[unmanaged] got x=%d y=%d\n", loc3.x, loc3.y);

    return 0;
}

#pragma managed

int main() {
   UnmanagedFunc();
}
```

## <a name="see-also"></a>См. также раздел

[Использование взаимодействия C++ (неявный PInvoke)](../dotnet/using-cpp-interop-implicit-pinvoke.md)
