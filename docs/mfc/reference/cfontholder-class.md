---
description: 'Дополнительные сведения о: Кфонсолдер Class'
title: Класс Кфонсолдер
ms.date: 11/04/2016
f1_keywords:
- CFontHolder
- AFXCTL/CFontHolder
- AFXCTL/CFontHolder::CFontHolder
- AFXCTL/CFontHolder::GetDisplayString
- AFXCTL/CFontHolder::GetFontDispatch
- AFXCTL/CFontHolder::GetFontHandle
- AFXCTL/CFontHolder::InitializeFont
- AFXCTL/CFontHolder::QueryTextMetrics
- AFXCTL/CFontHolder::ReleaseFont
- AFXCTL/CFontHolder::Select
- AFXCTL/CFontHolder::SetFont
- AFXCTL/CFontHolder::m_pFont
helpviewer_keywords:
- CFontHolder [MFC], CFontHolder
- CFontHolder [MFC], GetDisplayString
- CFontHolder [MFC], GetFontDispatch
- CFontHolder [MFC], GetFontHandle
- CFontHolder [MFC], InitializeFont
- CFontHolder [MFC], QueryTextMetrics
- CFontHolder [MFC], ReleaseFont
- CFontHolder [MFC], Select
- CFontHolder [MFC], SetFont
- CFontHolder [MFC], m_pFont
ms.assetid: 728ab472-0c97-440d-889f-1324c6e1b6b8
ms.openlocfilehash: 1670bd9a00c5b6f7990c15ba31d7256afb8d4031
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97184300"
---
# <a name="cfontholder-class"></a>Класс Кфонсолдер

Реализует свойство Font и инкапсулирует функциональность объекта шрифта Windows и интерфейса `IFont` .

## <a name="syntax"></a>Синтаксис

```
class CFontHolder
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[Кфонсолдер:: Кфонсолдер](#cfontholder)|Формирует объект `CFontHolder`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Кфонсолдер:: Жетдисплайстринг](#getdisplaystring)|Извлекает строку, отображаемую в обозревателе свойств контейнера.|
|[Кфонсолдер:: Жетфонтдиспатч](#getfontdispatch)|Возвращает `IDispatch` интерфейс шрифта.|
|[Кфонсолдер:: Жетфонсандле](#getfonthandle)|Возвращает маркер для шрифта Windows.|
|[Кфонсолдер:: Инитиализефонт](#initializefont)|Инициализирует объект `CFontHolder`.|
|[Кфонсолдер:: Куеритекстметрикс](#querytextmetrics)|Получает сведения для связанного шрифта.|
|[Кфонсолдер:: Релеасефонт](#releasefont)|Отключает `CFontHolder` объект от `IFont` `IFontNotification` интерфейсов и.|
|[Кфонсолдер:: SELECT](#select)|Выбирает ресурс шрифта в контексте устройства.|
|[Кфонсолдер:: Сетфонт](#setfont)|Подключает `CFontHolder` объект к `IFont` интерфейсу.|

### <a name="public-data-members"></a>Открытые члены данных

|Имя|Описание|
|----------|-----------------|
|[Кфонсолдер:: m_pFont](#m_pfont)|Указатель на `CFontHolder` `IFont` интерфейс объекта.|

## <a name="remarks"></a>Комментарии

`CFontHolder` не имеет базового класса.

Этот класс используется для реализации настраиваемых свойств шрифта для элемента управления. Сведения о создании таких свойств см. в статье [элементы управления ActiveX: использование шрифтов](../../mfc/mfc-activex-controls-using-fonts.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`CFontHolder`

## <a name="requirements"></a>Требования

**Заголовок:** afxctl. h

## <a name="cfontholdercfontholder"></a><a name="cfontholder"></a> Кфонсолдер:: Кфонсолдер

Формирует объект `CFontHolder`.

```
explicit CFontHolder(LPPROPERTYNOTIFYSINK pNotify);
```

### <a name="parameters"></a>Параметры

*пнотифи*<br/>
Указатель на `IPropertyNotifySink` интерфейс шрифта.

### <a name="remarks"></a>Комментарии

Необходимо вызвать метод `InitializeFont` , чтобы инициализировать полученный объект перед его использованием.

## <a name="cfontholdergetdisplaystring"></a><a name="getdisplaystring"></a> Кфонсолдер:: Жетдисплайстринг

Извлекает строку, которая может быть отображена в браузере свойств контейнера.

```
BOOL GetDisplayString(CString& strValue);
```

### <a name="parameters"></a>Параметры

*strValue*<br/>
Ссылка на [CString](../../atl-mfc-shared/reference/cstringt-class.md) , который будет содержать отображаемую строку.

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если строка успешно получена; в противном случае — 0.

## <a name="cfontholdergetfontdispatch"></a><a name="getfontdispatch"></a> Кфонсолдер:: Жетфонтдиспатч

Вызовите эту функцию, чтобы получить указатель на интерфейс диспетчеризации шрифта.

```
LPFONTDISP GetFontDispatch();
```

### <a name="return-value"></a>Возвращаемое значение

Указатель на `CFontHolder` `IFontDisp` интерфейс объекта. Обратите внимание, что функция, которая вызывает метод, `GetFontDispatch` должна вызывать `IUnknown::Release` для этого указателя интерфейса, когда это делается с ним.

### <a name="remarks"></a>Комментарии

Вызов `InitializeFont` перед вызовом `GetFontDispatch` .

## <a name="cfontholdergetfonthandle"></a><a name="getfonthandle"></a> Кфонсолдер:: Жетфонсандле

Вызовите эту функцию, чтобы получить маркер для шрифта Windows.

```
HFONT GetFontHandle();

HFONT GetFontHandle(
    long cyLogical,
    long cyHimetric);
```

### <a name="parameters"></a>Параметры

*цилогикал*<br/>
Высота прямоугольника, в котором рисуется элемент управления, в логических единицах.

*цихиметрик*<br/>
Высота элемента управления в MM_HIMETRIC единицах.

### <a name="return-value"></a>Возвращаемое значение

Маркер объекта Font; в противном случае — NULL.

### <a name="remarks"></a>Комментарии

Отношение *цилогикал* и *цихиметрик* используется для вычисления правильного размера отображения в логических единицах для размера кегля шрифта, выраженного в единицах MM_HIMETRIC:

Размер дисплея = ( *цилогикал*  /  *цихиметрик*) X размер шрифта

Версия без параметров возвращает маркер для правильного размера шрифта на экране.

## <a name="cfontholderinitializefont"></a><a name="initializefont"></a> Кфонсолдер:: Инитиализефонт

Инициализирует объект `CFontHolder`.

```cpp
void InitializeFont(
    const FONTDESC* pFontDesc = NULL,
    LPDISPATCH pFontDispAmbient = NULL);
```

### <a name="parameters"></a>Параметры

*пфонтдеск*<br/>
Указатель на структуру описания шрифта ( [фонтдеск](/windows/win32/api/olectl/ns-olectl-fontdesc)), указывающую характеристики шрифта.

*пфонтдиспамбиент*<br/>
Указатель на свойство внешнего шрифта контейнера.

### <a name="remarks"></a>Комментарии

Если *пфонтдиспамбиент* не равно null, `CFontHolder` объект подключается к клону интерфейса, `IFont` используемого свойством Font внешнего шрифта контейнера.

Если *пфонтдиспамбиент* имеет значение null, создается новый объект Font либо из описания шрифта, на которое указывает *пфонтдеск* , либо, если *пфонтдеск* имеет значение null, из описания по умолчанию.

Вызовите эту функцию после создания `CFontHolder` объекта.

## <a name="cfontholderm_pfont"></a><a name="m_pfont"></a> Кфонсолдер:: m_pFont

Указатель на `CFontHolder` `IFont` интерфейс объекта.

```
LPFONT m_pFont;
```

## <a name="cfontholderquerytextmetrics"></a><a name="querytextmetrics"></a> Кфонсолдер:: Куеритекстметрикс

Получает сведения о физическом шрифте, представленном `CFontHolder` объектом.

```cpp
void QueryTextMetrics(LPTEXTMETRIC lptm);
```

### <a name="parameters"></a>Параметры

*лптм*<br/>
Указатель на структуру [текстметрик](/windows/win32/api/wingdi/ns-wingdi-textmetricw) , которая будет принимать сведения.

## <a name="cfontholderreleasefont"></a><a name="releasefont"></a> Кфонсолдер:: Релеасефонт

Эта функция отключает `CFontHolder` объект от своего `IFont` интерфейса.

```cpp
void ReleaseFont();
```

## <a name="cfontholderselect"></a><a name="select"></a> Кфонсолдер:: SELECT

Вызовите эту функцию, чтобы выбрать шрифт элемента управления в указанном контексте устройства.

```
CFont* Select(
    CDC* pDC,
    long cyLogical,
    long cyHimetric);
```

### <a name="parameters"></a>Параметры

*Хозяин*<br/>
Контекст устройства, в котором выбран шрифт.

*цилогикал*<br/>
Высота прямоугольника, в котором рисуется элемент управления, в логических единицах.

*цихиметрик*<br/>
Высота элемента управления в MM_HIMETRIC единицах.

### <a name="return-value"></a>Возвращаемое значение

Указатель на заменяемый шрифт.

### <a name="remarks"></a>Комментарии

Описание параметров *цилогикал* и *цихиметрик* см. в разделе [жетфонсандле](#getfonthandle) .

## <a name="cfontholdersetfont"></a><a name="setfont"></a> Кфонсолдер:: Сетфонт

Освобождает существующий шрифт и подключает `CFontHolder` объект к `IFont` интерфейсу.

```cpp
void SetFont(LPFONT pNewFont);
```

### <a name="parameters"></a>Параметры

*пневфонт*<br/>
Указатель на новый `IFont` интерфейс.

## <a name="see-also"></a>См. также раздел

[Иерархическая диаграмма](../../mfc/hierarchy-chart.md)<br/>
[Класс Кпропексчанже](../../mfc/reference/cpropexchange-class.md)
