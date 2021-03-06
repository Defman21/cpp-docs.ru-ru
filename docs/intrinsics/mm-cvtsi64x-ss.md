---
description: 'Дополнительные сведения: _mm_cvtsi64x_ss'
title: _mm_cvtsi64x_ss
ms.date: 09/02/2019
f1_keywords:
- _mm_cvtsi64x_ss
helpviewer_keywords:
- cvtsi2ss instruction
- _mm_cvtsi64x_ss intrinsic
ms.assetid: 01e5d321-c18a-46fd-a6f6-324364514e1f
ms.openlocfilehash: 81a1af04d4c66cefd9815471baeb3a6095403ddf
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97167725"
---
# <a name="_mm_cvtsi64x_ss"></a>_mm_cvtsi64x_ss

**Блок, относящийся только к системам Microsoft**

Создает расширенную версию 64-разрядной версии преобразования 64 бит, которая преобразуется в скалярную инструкцию Single-Precision Floating-Point value ( `cvtsi2ss` ).

## <a name="syntax"></a>Синтаксис

```C
__m128 _mm_cvtsi64x_ss(
   __m128 a,
   __int64 b
);
```

### <a name="parameters"></a>Параметры

*конкретного*\
окне **`__m128`** Структура, содержащая четыре значения с плавающей запятой одиночной точности.

*&*\
окне 64-разрядное целое число, которое преобразуется в значение с плавающей запятой.

## <a name="return-value"></a>Возвращаемое значение

**`__m128`** Структура, первое значение с плавающей запятой которой является результатом преобразования. Остальные три значения копируются без *изменений из.*

## <a name="requirements"></a>Требования

|Intrinsic|Архитектура|
|---------------|------------------|
|`_mm_cvtsi64x_ss`|X64|

**Файл заголовка** \<intrin.h>

## <a name="remarks"></a>Комментарии

**`__m128`** Структура представляет регистр XMM, поэтому встроенное позволяет переместить значение *b* из системной памяти в регистр XMM.

Эта процедура доступна только как встроенная функция.

## <a name="example"></a>Пример

```cpp
// _mm_cvtsi64x_ss.cpp
// processor: x64

#include <intrin.h>
#include <stdio.h>

#pragma intrinsic(_mm_cvtsi64x_ss)

int main()
{
    __m128 a;
    __int64 b = 54;

    a.m128_f32[0] = 0;
    a.m128_f32[1] = 0;
    a.m128_f32[2] = 0;
    a.m128_f32[3] = 0;
    a = _mm_cvtsi64x_ss(a, b);

    printf_s( "%lf %lf %lf %lf\n",
              a.m128_f32[0], a.m128_f32[1],
              a.m128_f32[2], a.m128_f32[3] );
}
```

```Output
54.000000 0.000000 0.000000 0.000000
```

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[__m128](../cpp/m128.md)\
[Встроенные объекты компилятора](../intrinsics/compiler-intrinsics.md)
