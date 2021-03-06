---
description: 'Дополнительные сведения о: CW2AEX Class'
title: Класс CW2AEX
ms.date: 11/04/2016
f1_keywords:
- CW2AEX
- ATLCONV/ATL::CW2AEX
- ATLCONV/ATL::CW2AEX::CW2AEX
- ATLCONV/ATL::CW2AEX::m_psz
- ATLCONV/ATL::CW2AEX::m_szBuffer
helpviewer_keywords:
- CW2AEX class
ms.assetid: 44dc2cf5-dd30-440b-a9b9-b21b43f49843
ms.openlocfilehash: dfb654c43f2549cc1cfe58be064b2e6b9621fc69
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97140287"
---
# <a name="cw2aex-class"></a>Класс CW2AEX

Этот класс используется макросами преобразования строк CT2AEX, CW2TEX, CW2CTEX и CT2CAEX и typedef CW2A.

> [!IMPORTANT]
> Этот класс и его члены не могут использоваться в приложениях, выполняемых в среда выполнения Windows.

## <a name="syntax"></a>Синтаксис

```
template<int t_nBufferLength = 128>
class CW2AEX
```

#### <a name="parameters"></a>Параметры

*t_nBufferLength*<br/>
Размер буфера, используемого в процессе перевода. Длина по умолчанию составляет 128 байт.

## <a name="members"></a>Элементы

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[CW2AEX::CW2AEX](#cw2aex)|Конструктор.|
|[CW2AEX:: ~ CW2AEX](#dtor)|Деструктор|

### <a name="public-operators"></a>Открытые операторы

|Имя|Описание|
|----------|-----------------|
|[CW2AEX:: operator LPSTR](#operator_lpstr)|Оператор преобразования.|

### <a name="public-data-members"></a>Открытые члены данных

|Имя|Описание|
|----------|-----------------|
|[CW2AEX:: m_psz](#m_psz)|Элемент данных, в котором хранится исходная строка.|
|[CW2AEX:: m_szBuffer](#m_szbuffer)|Статический буфер, используемый для хранения преобразованной строки.|

## <a name="remarks"></a>Комментарии

Если не требуется дополнительных функций, используйте в коде CT2AEX, CW2TEX, CW2CTEX, CT2CAEX или CW2A.

Этот класс содержит статический буфер фиксированного размера, который используется для хранения результата преобразования. Если результат слишком велик для использования в статическом буфере, класс выделяет память с помощью функции **malloc**, освобождая память, когда объект выходит из области. Это гарантирует, что, в отличие от макросов преобразования текста, доступных в предыдущих версиях ATL, этот класс можно использовать в циклах, и он не будет переполнен стек.

Если класс пытается выделить память в куче и завершается ошибкой, он вызывается `AtlThrow` с аргументом E_OUTOFMEMORY.

По умолчанию классы и макросы преобразования ATL используют для преобразования кодовую страницу ANSI текущего потока. Если вы хотите переопределить это поведение для конкретного преобразования, укажите кодовую страницу в качестве второго параметра для конструктора класса.

Следующие макросы основаны на этом классе:

- CT2AEX

- CW2TEX

- CW2CTEX

- CT2CAEX

Следующий typedef основан на этом классе:

- CW2A

Обсуждение этих макросов преобразования текста см. в разделе [ATL и макросы преобразования строк MFC](string-conversion-macros.md).

## <a name="example"></a>Пример

Пример использования этих макросов преобразования строк см. в разделе [ATL и макросы преобразования строк MFC](string-conversion-macros.md) .

## <a name="requirements"></a>Требования

**Заголовок:** атлконв. h

## <a name="cw2aexcw2aex"></a><a name="cw2aex"></a> CW2AEX::CW2AEX

Конструктор.

```
CW2AEX(LPCWSTR psz, UINT nCodePage) throw(...);
CW2AEX(LPCWSTR psz) throw(...);
```

### <a name="parameters"></a>Параметры

*псз*<br/>
Текстовая строка для преобразования.

*нкодепаже*<br/>
Кодовая страница, используемая для выполнения преобразования. Дополнительные сведения см. в обсуждении параметров кодовой страницы для функции Windows SDK [MultiByteToWideChar](/windows/win32/api/stringapiset/nf-stringapiset-multibytetowidechar) .

### <a name="remarks"></a>Комментарии

Выделяет буфер, используемый в процессе перевода.

## <a name="cw2aexcw2aex"></a><a name="dtor"></a> CW2AEX:: ~ CW2AEX

Деструктор

```
~CW2AEX() throw();
```

### <a name="remarks"></a>Комментарии

Освобождает выделенный буфер.

## <a name="cw2aexm_psz"></a><a name="m_psz"></a> CW2AEX:: m_psz

Элемент данных, в котором хранится исходная строка.

```
LPSTR m_psz;
```

## <a name="cw2aexm_szbuffer"></a><a name="m_szbuffer"></a> CW2AEX:: m_szBuffer

Статический буфер, используемый для хранения преобразованной строки.

```
char m_szBuffer[t_nBufferLength];
```

## <a name="cw2aexoperator-lpstr"></a><a name="operator_lpstr"></a> CW2AEX:: operator LPSTR

Оператор преобразования.

```
operator LPSTR() const throw();
```

### <a name="return-value"></a>Возвращаемое значение

Возвращает текстовую строку как тип LPSTR.

## <a name="see-also"></a>См. также раздел

[Класс CA2AEX](../../atl/reference/ca2aex-class.md)<br/>
[Класс CA2CAEX](../../atl/reference/ca2caex-class.md)<br/>
[Класс CA2WEX](../../atl/reference/ca2wex-class.md)<br/>
[Класс CW2CWEX](../../atl/reference/cw2cwex-class.md)<br/>
[Класс CW2WEX](../../atl/reference/cw2wex-class.md)<br/>
[Общие сведения о классах](../../atl/atl-class-overview.md)
