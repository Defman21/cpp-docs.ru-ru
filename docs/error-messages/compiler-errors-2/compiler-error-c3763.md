---
description: 'Дополнительные сведения о: Ошибка компилятора C3763'
title: Ошибка компилятора C3763
ms.date: 11/04/2016
f1_keywords:
- C3763
helpviewer_keywords:
- C3763
ms.assetid: 58b1f079-cd1d-46e0-9431-ea18210106b7
ms.openlocfilehash: 9423c2f0db133c58fc7680b475a450c7190423f4
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97285439"
---
# <a name="compiler-error-c3763"></a>Ошибка компилятора C3763

"тип": "retval" и "out" могут использоваться только в типе указателя данных

Атрибуты [out](../../windows/attributes/out-cpp.md) и [retval](../../windows/attributes/retval.md) могут присутствовать только в параметрах типа pointer. Удалите атрибут или установите параметр указателя типа.

Следующий пример приводит к возникновению ошибки C3763:

```cpp
// C3763.cpp
#define _ATL_ATTRIBUTES 1
#include <atlbase.h>
#include <atlplus.h>
#include <atlcom.h>

[ module(name=test) ];

[ dispinterface, uuid("00000000-0000-0000-0000-000000000001") ]
__interface IF84 : IDispatch
{
   [id(0x00000002)]HRESULT m2([out]unsigned char);
};

[ coclass, uuid("00000000-0000-0000-0000-000000000002") ]
class CF84 : public IF84
{   // C3763
public:
   HRESULT __stdcall m2(unsigned char i)
   {
      return S_OK;
   }
};

int main()
{
}
```
