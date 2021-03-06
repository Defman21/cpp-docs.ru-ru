---
description: 'Дополнительные сведения о: Кфонтдиалог Class'
title: Класс Кфонтдиалог
ms.date: 11/04/2016
f1_keywords:
- CFontDialog
- AFXDLGS/CFontDialog
- AFXDLGS/CFontDialog::CFontDialog
- AFXDLGS/CFontDialog::DoModal
- AFXDLGS/CFontDialog::GetCharFormat
- AFXDLGS/CFontDialog::GetColor
- AFXDLGS/CFontDialog::GetCurrentFont
- AFXDLGS/CFontDialog::GetFaceName
- AFXDLGS/CFontDialog::GetSize
- AFXDLGS/CFontDialog::GetStyleName
- AFXDLGS/CFontDialog::GetWeight
- AFXDLGS/CFontDialog::IsBold
- AFXDLGS/CFontDialog::IsItalic
- AFXDLGS/CFontDialog::IsStrikeOut
- AFXDLGS/CFontDialog::IsUnderline
- AFXDLGS/CFontDialog::m_cf
helpviewer_keywords:
- CFontDialog [MFC], CFontDialog
- CFontDialog [MFC], DoModal
- CFontDialog [MFC], GetCharFormat
- CFontDialog [MFC], GetColor
- CFontDialog [MFC], GetCurrentFont
- CFontDialog [MFC], GetFaceName
- CFontDialog [MFC], GetSize
- CFontDialog [MFC], GetStyleName
- CFontDialog [MFC], GetWeight
- CFontDialog [MFC], IsBold
- CFontDialog [MFC], IsItalic
- CFontDialog [MFC], IsStrikeOut
- CFontDialog [MFC], IsUnderline
- CFontDialog [MFC], m_cf
ms.assetid: 6228d500-ed0f-4156-81e5-ab0d57d1dcf4
ms.openlocfilehash: c1f8637a6106db9220721dffe67a2ed1d53b26b7
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97184352"
---
# <a name="cfontdialog-class"></a>Класс Кфонтдиалог

Позволяет включить в приложение диалоговое окно выбора шрифта.

## <a name="syntax"></a>Синтаксис

```
class CFontDialog : public CCommonDialog
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[Кфонтдиалог:: Кфонтдиалог](#cfontdialog)|Формирует объект `CFontDialog`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Кфонтдиалог::D Омодал](#domodal)|Отображает диалоговое окно и позволяет пользователю сделать выбор.|
|[Кфонтдиалог:: Жетчарформат](#getcharformat)|Извлекает форматирование символов выбранного шрифта.|
|[Кфонтдиалог:: "Color"](#getcolor)|Возвращает цвет выбранного шрифта.|
|[Кфонтдиалог:: Жеткуррентфонт](#getcurrentfont)|Назначает характеристики выбранного в данный момент шрифта `LOGFONT` структуре.|
|[Кфонтдиалог:: Жетфаценаме](#getfacename)|Возвращает название выбранного шрифта.|
|[Кфонтдиалог:: DataSize](#getsize)|Возвращает размер выбранного шрифта в виде точки.|
|[Кфонтдиалог:: Жетстиленаме](#getstylename)|Возвращает имя стиля выбранного шрифта.|
|[Кфонтдиалог:: масса](#getweight)|Возвращает вес выбранного шрифта.|
|[Кфонтдиалог:: Bold](#isbold)|Определяет, является ли шрифт полужирным.|
|[Кфонтдиалог:: Italic](#isitalic)|Определяет, является ли шрифт курсивом.|
|[Кфонтдиалог:: зачеркнутый](#isstrikeout)|Определяет, отображается ли шрифт с зачеркиванием.|
|[Кфонтдиалог:: подчеркивание](#isunderline)|Определяет, является ли шрифт подчеркнутым.|

### <a name="public-data-members"></a>Открытые члены данных

|Имя|Описание|
|----------|-----------------|
|[Кфонтдиалог:: m_cf](#m_cf)|Структура, используемая для настройки `CFontDialog` объекта.|

## <a name="remarks"></a>Комментарии

`CFontDialog`Объект — это диалоговое окно со списком шрифтов, установленных в системе в настоящий момент. Пользователь может выбрать определенный шрифт из списка, после чего этот выбор будет возвращен в приложение.

Для создания `CFontDialog` объекта используйте предоставленный конструктор или создайте производный от него новый подкласс и используйте собственный пользовательский конструктор.

После создания `CFontDialog` объекта можно использовать `m_cf` структуру для инициализации значений или состояний элементов управления в диалоговом окне. Структура [m_cf](#m_cf) имеет тип [CHOOSEFONT](/windows/win32/api/commdlg/ns-commdlg-choosefontw). Дополнительные сведения об этой структуре см. в Windows SDK.

После инициализации элементов управления диалогового окна вызовите `DoModal` функцию-член, чтобы отобразить диалоговое окно и позволить пользователю выбрать шрифт. `DoModal` Возвращает значение, указывающее, выбрал пользователь кнопку ОК (ИДОК) или Отмена (ИДКАНЦЕЛ).

Если `DoModal` функция ВОЗВРАЩАЕТ идок, `CFontDialog` для получения входных данных пользователем можно использовать одну из функций члена.

Вы можете использовать функцию Windows [коммдлжекстендедеррор](/windows/win32/api/commdlg/nf-commdlg-commdlgextendederror) , чтобы определить, произошла ли ошибка во время инициализации диалогового окна, и получить дополнительные сведения об ошибке. Дополнительные сведения об этой функции см. в Windows SDK.

`CFontDialog` зависит от файла COMMDLG.DLL, поставляемого с Windows версии 3,1 и более поздних версий.

Чтобы настроить диалоговое окно, создайте производный класс от `CFontDialog` , предоставьте пользовательский шаблон диалогового окна и добавьте карту сообщений для обработки сообщений уведомлений из расширенных элементов управления. Все необработанные сообщения должны передаваться в базовый класс.

Настройка функции-обработчика не является обязательной.

Дополнительные сведения об использовании см `CFontDialog` . в разделе [Общие классы диалоговых окон](../../mfc/common-dialog-classes.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CWnd](../../mfc/reference/cwnd-class.md)

[CDialog](../../mfc/reference/cdialog-class.md)

[CCommonDialog](../../mfc/reference/ccommondialog-class.md)

`CFontDialog`

## <a name="requirements"></a>Требования

**Заголовок:** афксдлгс. h

## <a name="cfontdialogcfontdialog"></a><a name="cfontdialog"></a> Кфонтдиалог:: Кфонтдиалог

Формирует объект `CFontDialog`.

```
CFontDialog(
    LPLOGFONT lplfInitial = NULL,
    DWORD dwFlags = CF_EFFECTS | CF_SCREENFONTS,
    CDC* pdcPrinter = NULL,
    CWnd* pParentWnd = NULL);

CFontDialog(
    const CHARFORMAT& charformat,
    DWORD dwFlags = CF_SCREENFONTS,
    CDC* pdcPrinter = NULL,
    CWnd* pParentWnd = NULL);
```

### <a name="parameters"></a>Параметры

*плфинитиал*<br/>
Указатель на структуру данных [LOGFONT](/windows/win32/api/wingdi/ns-wingdi-logfontw) , которая позволяет задать некоторые характеристики шрифта.

*чарформат*<br/>
Указатель на структуру данных [чарформат](/windows/win32/api/richedit/ns-richedit-charformata) , которая позволяет задать некоторые характеристики шрифта в элементе управления Rich Edit.

*dwFlags*<br/>
Указывает один или несколько флагов выбора шрифта. Одно или несколько предустановленных значений можно объединить с помощью побитового оператора OR. Если вы изменяете член структуры `m_cf.Flag`, используйте оператор OR в изменениях, чтобы сохранить поведение по умолчанию. Дополнительные сведения о каждом из этих флагов см. в описании структуры [CHOOSEFONT](/windows/win32/api/commdlg/ns-commdlg-choosefontw) в Windows SDK.

*пдкпринтер*<br/>
Указатель на контекст принтера. Если этот параметр задан, он указывает на контекст принтера, для которого выбираются шрифты.

*ппарентвнд*<br/>
Указатель на родительское окно или окно владельца диалогового окна шрифта.

### <a name="remarks"></a>Комментарии

Обратите внимание, что конструктор автоматически заполняет члены структуры `CHOOSEFONT`. Их следует изменять, только если вам требуется диалоговое окно, отличное от стандартного.

> [!NOTE]
> Первая версия этой функции существует, только если элементы управления форматированным редактированием не поддерживаются.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#78](../../mfc/codesnippet/cpp/cfontdialog-class_1.cpp)]

## <a name="cfontdialogdomodal"></a><a name="domodal"></a> Кфонтдиалог::D Омодал

Вызовите эту функцию, чтобы отобразить диалоговое окно "общий шрифт Windows" и позволить пользователю выбрать шрифт.

```
virtual INT_PTR DoModal();
```

### <a name="return-value"></a>Возвращаемое значение

ИДОК или ИДКАНЦЕЛ. Если возвращается ИДКАНЦЕЛ, вызовите функцию Windows [коммдлжекстендедеррор](/windows/win32/api/commdlg/nf-commdlg-commdlgextendederror) , чтобы определить, произошла ли ошибка.

ИДОК и ИДКАНЦЕЛ — это константы, которые указывают, выбрал ли пользователь кнопку ОК или Отмена.

### <a name="remarks"></a>Комментарии

Если вы хотите инициализировать различные элементы управления диалогового окна шрифта путем установки элементов структуры [m_cf](#m_cf) , это следует сделать перед вызовом метода `DoModal` , но после создания объекта диалогового окна.

Если `DoModal` ВОЗВРАЩАЕТ идок, можно вызвать другие функции члена для получения параметров или данных, вводимых пользователем, в диалоговое окно.

### <a name="example"></a>Пример

  См. примеры для [кфонтдиалог:: кфонтдиалог](#cfontdialog) и [кфонтдиалог:: "Color"](#getcolor).

## <a name="cfontdialoggetcharformat"></a><a name="getcharformat"></a> Кфонтдиалог:: Жетчарформат

Извлекает форматирование символов выбранного шрифта.

```cpp
void GetCharFormat(CHARFORMAT& cf) const;
```

### <a name="parameters"></a>Параметры

*CF*<br/>
Структура [чарформат](/windows/win32/api/richedit/ns-richedit-charformata) , содержащая сведения о форматировании символов выбранного шрифта.

## <a name="cfontdialoggetcolor"></a><a name="getcolor"></a> Кфонтдиалог:: "Color"

Вызовите эту функцию, чтобы получить выбранный цвет шрифта.

```
COLORREF GetColor() const;
```

### <a name="return-value"></a>Возвращаемое значение

Цвет выбранного шрифта.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#79](../../mfc/codesnippet/cpp/cfontdialog-class_2.cpp)]

## <a name="cfontdialoggetcurrentfont"></a><a name="getcurrentfont"></a> Кфонтдиалог:: Жеткуррентфонт

Вызывайте эту функцию, чтобы назначить характеристики выбранного в данный момент шрифта элементам структуры [LOGFONT](/windows/win32/api/wingdi/ns-wingdi-logfontw) .

```cpp
void GetCurrentFont(LPLOGFONT lplf);
```

### <a name="parameters"></a>Параметры

*лплф*<br/>
Указатель на `LOGFONT` структуру.

### <a name="remarks"></a>Комментарии

`CFontDialog`Для доступа к отдельным характеристикам текущего шрифта предоставляются другие функции элементов.

Если эта функция вызывается во время вызова [DoModal](#domodal), она возвращает текущее выделение во время (то, что пользователь видит или изменил в диалоговом окне). Если эта функция вызывается после вызова `DoModal` (только `DoModal` в случае, если возвращает идок), то возвращается то, что выделено пользователем.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#80](../../mfc/codesnippet/cpp/cfontdialog-class_3.cpp)]

## <a name="cfontdialoggetfacename"></a><a name="getfacename"></a> Кфонтдиалог:: Жетфаценаме

Вызовите эту функцию, чтобы получить название начертания выбранного шрифта.

```
CString GetFaceName() const;
```

### <a name="return-value"></a>Возвращаемое значение

Название начертания шрифта, выбранного в `CFontDialog` диалоговом окне.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#81](../../mfc/codesnippet/cpp/cfontdialog-class_4.cpp)]

## <a name="cfontdialoggetsize"></a><a name="getsize"></a> Кфонтдиалог:: DataSize

Вызовите эту функцию, чтобы получить размер выбранного шрифта.

```
int GetSize() const;
```

### <a name="return-value"></a>Возвращаемое значение

Размер шрифта в десятых долях точки.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#82](../../mfc/codesnippet/cpp/cfontdialog-class_5.cpp)]

## <a name="cfontdialoggetstylename"></a><a name="getstylename"></a> Кфонтдиалог:: Жетстиленаме

Вызовите эту функцию, чтобы получить имя стиля выбранного шрифта.

```
CString GetStyleName() const;
```

### <a name="return-value"></a>Возвращаемое значение

Имя стиля шрифта.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#83](../../mfc/codesnippet/cpp/cfontdialog-class_6.cpp)]

## <a name="cfontdialoggetweight"></a><a name="getweight"></a> Кфонтдиалог:: масса

Вызовите эту функцию, чтобы получить весовой коэффициент выбранного шрифта.

```
int GetWeight() const;
```

### <a name="return-value"></a>Возвращаемое значение

Вес выбранного шрифта.

### <a name="remarks"></a>Комментарии

Дополнительные сведения о весе шрифта см. в разделе [кфонт:: CreateFont](../../mfc/reference/cfont-class.md#createfont).

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#84](../../mfc/codesnippet/cpp/cfontdialog-class_7.cpp)]

## <a name="cfontdialogisbold"></a><a name="isbold"></a> Кфонтдиалог:: Bold

Вызовите эту функцию, чтобы определить, является ли выбранный шрифт полужирным.

```
BOOL IsBold() const;
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если для выбранного шрифта включено выделение полужирным шрифтом; в противном случае — 0.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#85](../../mfc/codesnippet/cpp/cfontdialog-class_8.cpp)]

## <a name="cfontdialogisitalic"></a><a name="isitalic"></a> Кфонтдиалог:: Italic

Вызовите эту функцию, чтобы определить, является ли выбранный шрифт курсивом.

```
BOOL IsItalic() const;
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если для выбранного шрифта включена характеристика курсива. в противном случае — 0.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#86](../../mfc/codesnippet/cpp/cfontdialog-class_9.cpp)]

## <a name="cfontdialogisstrikeout"></a><a name="isstrikeout"></a> Кфонтдиалог:: зачеркнутый

Вызовите эту функцию, чтобы определить, отображается ли выбранный шрифт с зачеркиванием.

```
BOOL IsStrikeOut() const;
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если для выбранного шрифта включена характеристика зачеркивания; в противном случае — 0.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#87](../../mfc/codesnippet/cpp/cfontdialog-class_10.cpp)]

## <a name="cfontdialogisunderline"></a><a name="isunderline"></a> Кфонтдиалог:: подчеркивание

Вызовите эту функцию, чтобы определить, подчеркнут ли выбранный шрифт.

```
BOOL IsUnderline() const;
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если для выбранного шрифта включена характеристика подчеркивания; в противном случае — 0.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#88](../../mfc/codesnippet/cpp/cfontdialog-class_11.cpp)]

## <a name="cfontdialogm_cf"></a><a name="m_cf"></a> Кфонтдиалог:: m_cf

Структура, члены которой хранят характеристики объекта диалогового окна.

```
CHOOSEFONT m_cf;
```

### <a name="remarks"></a>Комментарии

После создания `CFontDialog` объекта можно использовать `m_cf` для изменения различных аспектов диалогового окна перед вызовом `DoModal` функции-члена. Дополнительные сведения об этой структуре см. в разделе [CHOOSEFONT](/windows/win32/api/commdlg/ns-commdlg-choosefontw) в Windows SDK.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCDocView#89](../../mfc/codesnippet/cpp/cfontdialog-class_12.cpp)]

## <a name="see-also"></a>См. также раздел

[Пример MFC для примера HIERSVR](../../overview/visual-cpp-samples.md)<br/>
[Класс Ккоммондиалог](../../mfc/reference/ccommondialog-class.md)<br/>
[Иерархическая диаграмма](../../mfc/hierarchy-chart.md)
