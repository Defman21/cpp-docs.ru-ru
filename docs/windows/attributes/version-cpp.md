---
description: 'Дополнительные сведения: версия (C++)'
title: версия (атрибут COM C++)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.version
helpviewer_keywords:
- version attribute
- version information, version attribute
ms.assetid: db6ce5d8-82c2-4329-b1a8-8ca2f67342cb
ms.openlocfilehash: 5b6d13e59b36fe37d71c9e2cca6fe7d75587f77b
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97118307"
---
# <a name="version-c"></a>version (C++)

Определяет определенную версию для нескольких версий класса.

## <a name="syntax"></a>Синтаксис

```cpp
[ version("version") ]
```

### <a name="parameters"></a>Параметры

*version*<br/>
Номер версии `coclass`. Если не указано, 1,0 будет помещена в IDL-файл.

## <a name="remarks"></a>Комментарии

Атрибут **Version** C++ имеет те же функциональные возможности, что и атрибут MIDL [версии](/windows/win32/Midl/version) , и передается в созданный IDL-файл.

## <a name="example"></a>Пример

Пример использования **версии** см. в примере с [возможностью привязки](bindable.md) .

## <a name="requirements"></a>Требования

| Контекст атрибута | Значение |
|-|-|
|**Относится к**|**`class`**, **`struct`**|
|**REPEATABLE**|Нет|
|**Требуемые атрибуты**|**кокласс**|
|**Недопустимые атрибуты**|Нет|

Дополнительные сведения о контекстах атрибутов см. в разделе [Контексты атрибутов](cpp-attributes-com-net.md#contexts).

## <a name="see-also"></a>См. также раздел

[Атрибуты компилятора](compiler-attributes.md)<br/>
[Атрибуты класса](class-attributes.md)
