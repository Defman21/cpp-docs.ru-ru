---
description: 'Дополнительные сведения: _vfprintf_p, _vfprintf_p_l, _vfwprintf_p, _vfwprintf_p_l'
title: _vfprintf_p, _vfprintf_p_l, _vfwprintf_p, _vfwprintf_p_l
ms.date: 11/04/2016
api_name:
- _vfprintf_p
- _vfwprintf_p
- _vfprintf_p_l
- _vfwprintf_p_l
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
- _vfwprintf_p_l
- _vfprintf_p
- vfwprintf_p_l
- vfwprintf_p
- vfprintf_p_l
- _vfwprintf_p
- _vftprintf_p
- _vfprintf_p_l
- vfprintf_p
helpviewer_keywords:
- vfprintf_p_l function
- _vftprintf_p_l function
- _vfprintf_p function
- vfprintf_p function
- vftprintf_p_l function
- _vfprintf_p_l function
- _vftprintf_p function
- _vfwprintf_p_l function
- vfwprintf_p_l function
- _vfwprintf_p function
- vftprintf_p function
- formatted text [C++]
- vfwprintf_p function
ms.assetid: 4d4a0914-4175-4b65-9ca1-037c4ef29147
ms.openlocfilehash: 062fb24abb2f1b9032a462715585afc5a0dd23b6
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97340545"
---
# <a name="_vfprintf_p-_vfprintf_p_l-_vfwprintf_p-_vfwprintf_p_l"></a>_vfprintf_p, _vfprintf_p_l, _vfwprintf_p, _vfwprintf_p_l

Записывают форматированные выходные данные, используя указатель на список аргументов, с возможностью указать порядок, в котором эти аргументы используются в строке формата.

## <a name="syntax"></a>Синтаксис

```C
int _vfprintf_p(
   FILE *stream,
   const char *format,
   va_list argptr
);
int _vfprintf_p_l(
   FILE *stream,
   const char *format,
   locale_t locale,
   va_list argptr
);
int _vfwprintf_p(
   FILE *stream,
   const wchar_t *format,
   va_list argptr
);
int _vfwprintf_p_l(
   FILE *stream,
   const wchar_t *format,
   locale_t locale,
   va_list argptr
);
```

### <a name="parameters"></a>Параметры

*вышестоящий*<br/>
Указатель на структуру **FILE**.

*format*<br/>
Спецификация формата.

*аргптр*<br/>
Указатель на список аргументов.

*locale*<br/>
Используемый языковой стандарт.

Дополнительные сведения см. в разделе [Спецификации формата](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md).

## <a name="return-value"></a>Возвращаемое значение

**_vfprintf_p** и **_vfwprintf_p** возвращают число записанных символов, не включая завершающий нуль-символ, или отрицательное значение, если возникает ошибка вывода.

## <a name="remarks"></a>Комментарии

Каждая из этих функций принимает указатель на список аргументов, затем форматирует и записывает указанные данные в *поток*. Эти функции отличаются от **_vfprint_s** и **_vfwprint_s** версий только тем, что они поддерживают позиционированные параметры. Дополнительные сведения см. в разделе [Позиционные параметры printf_p](../../c-runtime-library/printf-p-positional-parameters.md).

**_vfwprintf_p** — это версия **_vprintf_p** для расширенных символов; Эти две функции ведут себя одинаково, если поток открыт в режиме ANSI. **_vprintf_p** в настоящее время не поддерживает вывод в поток Юникода.

Версии этих функций с суффиксом **_l** идентичны за исключением того, что они используют переданный параметр языкового стандарта вместо локали текущего потока.

> [!IMPORTANT]
> Убедитесь, что *format* не является строкой, определяемой пользователем. Дополнительные сведения см. в разделе [Как избежать переполнения буфера](/windows/win32/SecBP/avoiding-buffer-overruns).

Если *поток* или *Формат* является пустым указателем или строка формата содержит недопустимые символы форматирования, вызывается обработчик недопустимых параметров, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md). Если выполнение может быть продолжено, функции возвращают значение-1 и **задают значение** **еинвал**.

### <a name="generic-text-routine-mappings"></a>Универсальное текстовое сопоставление функций

|Подпрограмма TCHAR.H|_UNICODE и _MBCS не определены|_MBCS определено|_UNICODE определено|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_vftprintf_p**|**_vfprintf_p**|**_vfprintf_p**|**_vfwprintf_p**|
|**_vftprintf_p_l**|**_vfprintf_p_l**|**_vfprintf_p_l**|**_vfwprintf_p_l**|

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|Необязательные заголовки|
|-------------|---------------------|----------------------|
|**_vfprintf_p**, **_vfprintf_p_l**|\<stdio.h> и \<stdarg.h>|\<varargs.h>*|
|**_vfwprintf_p**, **_vfwprintf_p_l**|\<stdio.h> или \<wchar.h> , и \<stdarg.h>|\<varargs.h>*|

\* Требуется для совместимости с UNIX V.

Дополнительные сведения о совместимости см. в статье [Compatibility](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>См. также раздел

[Потоковый ввод-вывод](../../c-runtime-library/stream-i-o.md)<br/>
[Функции vprintf](../../c-runtime-library/vprintf-functions.md)<br/>
[fprintf, _fprintf_l, fwprintf, _fwprintf_l](fprintf-fprintf-l-fwprintf-fwprintf-l.md)<br/>
[printf, _printf_l, wprintf, _wprintf_l](printf-printf-l-wprintf-wprintf-l.md)<br/>
[sprintf, _sprintf_l, swprintf, _swprintf_l, \_ _swprintf_l](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[va_arg, va_copy, va_end, va_start](va-arg-va-copy-va-end-va-start.md)<br/>
[printf_p позиционированные параметры](../../c-runtime-library/printf-p-positional-parameters.md)<br/>
[_fprintf_p, _fprintf_p_l, _fwprintf_p, _fwprintf_p_l](fprintf-p-fprintf-p-l-fwprintf-p-fwprintf-p-l.md)<br/>
[_vsprintf_p, _vsprintf_p_l, _vswprintf_p, _vswprintf_p_l](vsprintf-p-vsprintf-p-l-vswprintf-p-vswprintf-p-l.md)<br/>
[_sprintf_p, _sprintf_p_l, _swprintf_p, _swprintf_p_l](sprintf-p-sprintf-p-l-swprintf-p-swprintf-p-l.md)<br/>
