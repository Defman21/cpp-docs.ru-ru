---
description: 'Дополнительные сведения: _set_printf_count_output'
title: _set_printf_count_output
ms.date: 11/04/2016
api_name:
- _set_printf_count_output
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
- api-ms-win-crt-stdio-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- set_printf_count_output
- _set_printf_count_output
helpviewer_keywords:
- '%n format'
- set_printf_count_output function
- _set_printf_count_output function
ms.assetid: d8259ec5-764e-42d0-9169-72172e95163b
ms.openlocfilehash: 455c4f0e49ce111853145a05d78efabcd76386fe
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97114251"
---
# <a name="_set_printf_count_output"></a>_set_printf_count_output

Включить или отключить поддержку формата **% n** в функциях [printf, _printf_l, wprintf, _wprintf_l](printf-printf-l-wprintf-wprintf-l.md)-Family.

## <a name="syntax"></a>Синтаксис

```C
int _set_printf_count_output(
   int enable
);
```

### <a name="parameters"></a>Параметры

*enable*<br/>
Ненулевое значение для включения поддержки **% n** , 0 для отключения поддержки **% n** .

## <a name="property-valuereturn-value"></a>Значение свойства/возвращаемое значение

Состояние **% n** поддержки перед вызовом этой функции: ненулевое значение, если включена поддержка **% n** , и 0, если она была отключена.

## <a name="remarks"></a>Комментарии

По соображениям безопасности поддержка описателя формата **% n** по умолчанию отключена в **printf** и всех ее вариантах. Если в спецификации формата **printf** обнаружено **% n** , поведение по умолчанию заключается в вызове обработчика недопустимых параметров, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md). Вызов **_set_printf_count_output** с ненулевым аргументом приведет к тому, что функции типа **printf**-Family будут интерпретировать **% n** , как описано в разделе [синтаксис спецификации формата: функции printf и wprintf](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md).

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**_set_printf_count_output**|\<stdio.h>|

Дополнительные сведения о совместимости см. в статье [Compatibility](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Пример

```C
// crt_set_printf_count_output.c
#include <stdio.h>

int main()
{
   int e;
   int i;
   e = _set_printf_count_output( 1 );
   printf( "%%n support was %sabled.\n",
        e ? "en" : "dis" );
   printf( "%%n support is now %sabled.\n",
        _get_printf_count_output() ? "en" : "dis" );
   printf( "12345%n6789\n", &i ); // %n format should set i to 5
   printf( "i = %d\n", i );
}
```

```Output
%n support was disabled.
%n support is now enabled.
123456789
i = 5
```

## <a name="see-also"></a>См. также раздел

[_get_printf_count_output](get-printf-count-output.md)<br/>
