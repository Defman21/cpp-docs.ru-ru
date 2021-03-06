---
title: Использование универсальных текстовых сопоставлений
description: Введение в сопоставления для типов данных, подпрограмм и других объектов в среде выполнения C, ориентированных на корпорацию Майкрософт.
ms.topic: conceptual
ms.date: 11/04/2016
f1_keywords:
- _UNICODE
helpviewer_keywords:
- _TXCHAR type
- TINT type
- _TCHAR type
- TSCHAR type
- TEXT type
- TCHAR type
- TCHAR.H data types, mappings defined in
- generic-text data types
- _TINT type
- TUCHAR type
- _UNICODE constant
- TXCHAR type
- generic-text mappings
- _TSCHAR type
- T type
- mappings, generic-text
- _TUCHAR type
- MBCS data type
- _MBCS data type
- _TEXT type
- UNICODE constant
- _T type
ms.assetid: 2848121c-e51f-4b9b-a2e6-833ece4b0cb3
ms.openlocfilehash: ea3b1eef413a0d9f52e81795c04424d533b83504
ms.sourcegitcommit: 9451db8480992017c46f9d2df23fb17b503bbe74
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590112"
---
# <a name="using-generic-text-mappings"></a>Использование универсальных текстовых сопоставлений

**Блок, относящийся только к системам Microsoft**

Чтобы упростить написание кода для разных международных рынков, в библиотеке времени выполнения Microsoft имеются специфичные для Microsoft "универсальные текстовые" сопоставления для многих типов данных, подпрограмм и других объектов. Эти сопоставления определяются в TCHAR.H. Данные сопоставления имен можно использовать для написания универсального кода, который можно компилировать в любом из трех типов наборов символов (ASCII (однобайтовая кодировка), многобайтовая кодировка или Юникод), в зависимости от константы манифеста, указанной с помощью оператора `#define`. Универсальные текстовые сопоставления представляют собой расширения Microsoft, несовместимые со стандартами ANSI.

### <a name="preprocessor-directives-for-generic-text-mappings"></a>Директивы препроцессора для универсальных текстовых сопоставлений

|#define|Скомпилированная версия|Пример|
|--------------|----------------------|-------------|
|`_UNICODE`|Юникод (расширенные символы)|`_tcsrev` соответствует `_wcsrev`|
|`_MBCS`|Многобайтовые символы|`_tcsrev` соответствует `_mbsrev`|
|Нет (по умолчанию: не определена ни константа `_UNICODE`, ни константа `_MBCS`)|Однобайтовая кодировка (ASCII)|`_tcsrev` соответствует `strrev`|

Например, определенная в файле TCHAR.H универсальная текстовая функция `_tcsrev` сопоставляется с функцией `mbsrev`, если в программе определена константа `MBCS`, или с функцией `_wcsrev`, если определена константа `_UNICODE`. В противном случае `_tcsrev` сопоставляется с `strrev`.

Тип данных Generic-Text `_TCHAR` , также определенный в файле Tchar. H, сопоставляет с типом **`char`** , если определен `_MBCS` , для типа, если **`wchar_t`** `_UNICODE` определено, и для типа, **`char`** Если ни одна константа не определена. Для удобства в файле TCHAR.H также предусмотрены другие сопоставления типов данных, однако `_TCHAR` является наиболее полезным типом.

### <a name="generic-text-data-type-mappings"></a>Сопоставления типов данных универсального текста

|Имя универсального текстового типа данных|Однобайтовая кодировка (_UNICODE, _MBCS не определены)|_MBCS определено|_UNICODE определено|
|----------------------------------|--------------------------------------------|--------------------|-----------------------|
|`_TCHAR`|**`char`**|**`char`**|**`wchar_t`**|
|`_TINT`|**`int`**|**`int`**|`wint_t`|
|`_TSCHAR`|**`signed char`**|**`signed char`**|**`wchar_t`**|
|`_TUCHAR`|**`unsigned char`**|**`unsigned char`**|**`wchar_t`**|
|`_TXCHAR`|**`char`**|**`unsigned char`**|**`wchar_t`**|
|`_T` или `_TEXT`|Не действует (удаляется препроцессором)|Не действует (удаляется препроцессором)|`L` (преобразует следующий символ или строку в аналог в Юникоде)|

Полный список универсальных текстовых сопоставлений для подпрограмм, переменных и других объектов см. в статье [Универсальные текстовые сопоставления](../c-runtime-library/generic-text-mappings.md).

В следующих примерах кода показано использование функций `_TCHAR` и `_tcsrev` для сопоставления моделям многобайтовой кодировки, Юникод и однобайтовой кодировки.

```
_TCHAR *RetVal, *szString;
RetVal = _tcsrev(szString);
```

Если указано `MBCS`, препроцессор сопоставляет предыдущий фрагмент следующему коду:

```
char *RetVal, *szString;
RetVal = _mbsrev(szString);
```

Если указано `_UNICODE`, препроцессор сопоставляет тот же фрагмент следующему коду:

```
wchar_t *RetVal, *szString;
RetVal = _wcsrev(szString);
```

Если не определена ни константа `_MBCS`, ни константа `_UNICODE`, препроцессор сопоставляет этот фрагмент коду в однобайтовой кодировке ASCII, как показано ниже:

```
char *RetVal, *szString;
RetVal = strrev(szString);
```

Таким образом, можно создавать, обслуживать и компилировать единый исходный файл кода, который будет выполняться с подпрограммами, использующими любую из трех описанных выше кодировок.

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[Универсальные текстовые сопоставления](../c-runtime-library/generic-text-mappings.md)<br/>
[Сопоставления типов данных](../c-runtime-library/data-type-mappings.md)<br/>
[Сопоставления констант и глобальных переменных](../c-runtime-library/constant-and-global-variable-mappings.md)<br/>
[Сопоставления подпрограмм](../c-runtime-library/routine-mappings.md)<br/>
[Пример программы с универсальным текстом](../c-runtime-library/a-sample-generic-text-program.md)
