---
description: 'Дополнительные сведения: implements_category'
title: implements_category (атрибут COM C++)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.implements_category
helpviewer_keywords:
- implements_category attribute
ms.assetid: fb162df3-1ebe-43dc-a084-668d7ef8c03f
ms.openlocfilehash: 0efc240394c67ab7d470523b8dfe5025b7a0f978
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97289547"
---
# <a name="implements_category"></a>implements_category

Указывает категории компонентов, реализуемых целевым классом.

## <a name="syntax"></a>Синтаксис

```cpp
[ implements_category(implements_category="uuid") ]
```

### <a name="parameters"></a>Параметры

*implements_category*<br/>
Идентификатор реализованной категории.

## <a name="remarks"></a>Комментарии

Атрибут **implements_category** C++ задает категории компонентов, реализуемых целевым классом. Это можно сделать, создав карту категорий и добавив отдельные записи, заданные атрибутом **implements_category** . Дополнительные сведения см. в разделах [категории компонентов и принципы их работы](/windows/win32/com/component-categories-and-how-they-work).

Этот атрибут требует, чтобы атрибут [coclass](coclass.md), [progid](progid.md)или [vi_progid](vi-progid.md) (или другой атрибут, который подразумевает один из них) также применялся к этому элементу. Если используется любой отдельный атрибут, два других применяются автоматически. Например, если `progid` применяется, то применяются `vi_progid` `coclass` также и.

## <a name="example"></a>Пример

Следующий код указывает, что следующий объект реализует `Control` категорию.

```cpp
// cpp_attr_ref_implements_category.cpp
// compile with: /LD
#define _ATL_ATTRIBUTES
#include "atlbase.h"
#include "atlcom.h"

[module (name="MyLib")];
[ coclass, implements_category("CATID_Control"),
  uuid("20a0d0cc-5172-40f5-99ae-5e032f3205ae")]
class CMyClass {};
```

## <a name="requirements"></a>Требования

| Контекст атрибута | Значение |
|-|-|
|**Относится к**|**`class`**, **`struct`**|
|**REPEATABLE**|Да|
|**Требуемые атрибуты**|Один из следующих элементов: `coclass` , `progid` или `vi_progid`|
|**Недопустимые атрибуты**|Нет|

Дополнительные сведения см. в разделе [Контексты атрибутов](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>См. также раздел

[Атрибуты COM](com-attributes.md)<br/>
[Атрибуты класса](class-attributes.md)<br/>
[IMPLEMENTED_CATEGORY](../../atl/reference/category-macros.md#implemented_category)
