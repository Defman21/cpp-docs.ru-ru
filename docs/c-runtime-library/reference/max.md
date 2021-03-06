---
description: 'Дополнительные сведения: __max'
title: __max
ms.date: 04/05/2018
api_name:
- __max
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- max
- __max
helpviewer_keywords:
- max macro
- maximum macro
- __max macro
ms.assetid: 05c936f6-0e22-45d6-a58d-4bc102e9dae2
ms.openlocfilehash: 709bbb7aee48e65fdd3feb21eb1984135faae2f1
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97299657"
---
# <a name="__max"></a>__max

Макрос препроцессора, который возвращает большее из двух значений.

## <a name="syntax"></a>Синтаксис

```C
#define __max(a,b) (((a) > (b)) ? (a) : (b))
```

### <a name="parameters"></a>Параметры

*a*, *b*<br/>
Сравниваемые значения любого числового типа данных.

## <a name="return-value"></a>Возвращаемое значение

**__max** возвращает больший из своих аргументов.

## <a name="remarks"></a>Комментарии

Макрос **__max** сравнивает два значения и возвращает значение больше единицы. Аргументы могут быть любого числового типа данных со знаком или без знака. Оба аргумента и возвращаемое значение должны принадлежать к одному типу данных.

Возвращаемый аргумент вычисляется дважды в макросе. Это может привести к непредвиденным результатам, если аргумент представляет собой выражение, изменяющее его значение при вычислении, например `*p++` .

## <a name="requirements"></a>Requirements (Требования)

|Макрос|Обязательный заголовок|
|-------------|---------------------|
|**__max**|\<stdlib.h>|

## <a name="example"></a>Пример

Дополнительные сведения см. в приведенных ниже примерах для функции [__min](min.md).

## <a name="see-also"></a>См. также раздел

[Поддержка операций с плавающей запятой](../../c-runtime-library/floating-point-support.md)<br/>
[__min](min.md)<br/>
