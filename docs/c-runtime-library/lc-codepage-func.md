---
description: 'Дополнительные сведения: ___lc_codepage_func'
title: ___lc_codepage_func
ms.date: 1/14/2021
api_name:
- ___lc_codepage_func
- _o____lc_codepage_func
api_location:
- msvcr120.dll
- msvcr110_clr0400.dll
- msvcr80.dll
- msvcr100.dll
- msvcr90.dll
- msvcr110.dll
- msvcrt.dll
- api-ms-win-crt-private-l1-1-0.dll
- api-ms-win-crt-locale-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- lc_codepage_func
- ___lc_codepage_func
helpviewer_keywords:
- ___lc_codepage_func
ms.assetid: 6a663bd0-5a63-4a2f-9507-872ec1582aae
ms.openlocfilehash: afe49a10498f65c01b501874b602079e79af3be8
ms.sourcegitcommit: 1cd8f8a75fd036ffa57bc70f3ca869042d8019d4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98242986"
---
# <a name="___lc_codepage_func"></a>___lc_codepage_func

Внутренняя функция CRT. Получает текущую кодовую страницу потока.

## <a name="syntax"></a>Синтаксис

```cpp
UINT ___lc_codepage_func(void);
```

## <a name="return-value"></a>Возвращаемое значение

Текущая кодовая страница потока.

## <a name="remarks"></a>Комментарии

`___lc_codepage_func` — это внутренняя функция CRT, которая используется другими функциями CRT для получения текущей кодовой страницы из локального хранилища потока для данных CRT. Эти сведения также доступны при использовании функции [_get_current_locale](../c-runtime-library/reference/get-current-locale.md).

*Кодовая страница* представляет собой сопоставление однобайтовых или двухбайтовых кодов с конкретными символами. Разные кодовые страницы включают разные специальные символы, как правило, настроенные для языка или группы языков. Дополнительные сведения о кодовых страницах см. в разделе [Code Pages](../c-runtime-library/code-pages.md).

Внутренние функции CRT связаны с конкретной реализацией и подлежат изменению в каждом выпуске. Мы не рекомендуем использовать их в коде.

По умолчанию глобальное состояние этой функции ограничивается приложением. Чтобы изменить это, см. раздел [глобальное состояние в CRT](global-state.md).

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|`___lc_codepage_func`|crt\src\setlocal.h|

## <a name="see-also"></a>См. также

[_get_current_locale](../c-runtime-library/reference/get-current-locale.md)<br/>
[setlocale, _wsetlocale](../c-runtime-library/reference/setlocale-wsetlocale.md)<br/>
[_create_locale, _wcreate_locale](../c-runtime-library/reference/create-locale-wcreate-locale.md)<br/>
[_free_locale](../c-runtime-library/reference/free-locale.md)
