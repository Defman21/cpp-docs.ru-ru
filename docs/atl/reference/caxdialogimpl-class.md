---
description: 'Дополнительные сведения о: Каксдиалогимпл Class'
title: Класс Каксдиалогимпл
ms.date: 11/04/2016
f1_keywords:
- CAxDialogImpl
- ATLWIN/ATL::CAxDialogImpl
- ATLWIN/ATL::CAxDialogImpl::AdviseSinkMap
- ATLWIN/ATL::CAxDialogImpl::Create
- ATLWIN/ATL::CAxDialogImpl::DestroyWindow
- ATLWIN/ATL::CAxDialogImpl::DoModal
- ATLWIN/ATL::CAxDialogImpl::EndDialog
- ATLWIN/ATL::CAxDialogImpl::GetDialogProc
- ATLWIN/ATL::CAxDialogImpl::GetIDD
- ATLWIN/ATL::CAxDialogImpl::IsDialogMessage
- ATLWIN/ATL::CAxDialogImpl::m_bModal
helpviewer_keywords:
- CAxDialogImpl class
- ATL, dialog boxes
ms.assetid: 817df483-3fa8-44e7-8487-72ba0881cd27
ms.openlocfilehash: e84ce636642ed268ec8ca0dd25e0f3c5f3bc10c0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97152455"
---
# <a name="caxdialogimpl-class"></a>Класс Каксдиалогимпл

Этот класс реализует диалоговое окно (модальное или немодальное), в котором размещены элементы управления ActiveX.

> [!IMPORTANT]
> Этот класс и его члены не могут использоваться в приложениях, выполняемых в среда выполнения Windows.

## <a name="syntax"></a>Синтаксис

```
template <class T, class TBase = CWindow>
class ATL_NO_VTABLE CAxDialogImpl : public CDialogImplBaseT<TBase>
```

#### <a name="parameters"></a>Параметры

*T*<br/>
Класс, производный от `CAxDialogImpl` .

*тбасе*<br/>
Базовый класс окна для `CDialogImplBaseT` .

## <a name="members"></a>Элементы

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Каксдиалогимпл:: Адвисесинкмап](#advisesinkmap)|Вызовите этот метод, чтобы рекомендовать или отменять все записи в сопоставлении событий в схеме приемника объекта.|
|[Каксдиалогимпл:: Create](#create)|Вызовите этот метод, чтобы создать немодальное диалоговое окно.|
|[Каксдиалогимпл::D Естройвиндов](#destroywindow)|Вызовите этот метод, чтобы уничтожить немодальное диалоговое окно.|
|[Каксдиалогимпл::D Омодал](#domodal)|Вызовите этот метод, чтобы создать модальное диалоговое окно.|
|[Каксдиалогимпл:: EndDialog](#enddialog)|Вызовите этот метод, чтобы уничтожить модальное диалоговое окно.|
|[Каксдиалогимпл:: Жетдиалогпрок](#getdialogproc)|Вызовите этот метод, чтобы получить указатель на `DialogProc` функцию обратного вызова.|
|[Каксдиалогимпл:: Жетидд](#getidd)|Вызовите этот метод, чтобы получить идентификатор ресурса шаблона диалогового окна|
|[Каксдиалогимпл:: Исдиалогмессаже](#isdialogmessage)|Вызовите этот метод, чтобы определить, предназначено ли сообщение для этого диалогового окна, и, если это так, обработать сообщение.|

### <a name="protected-data-members"></a>Защищенные члены данных

|Имя|Описание|
|----------|-----------------|
|[Каксдиалогимпл:: m_bModal](#m_bmodal)|Переменная, которая существует только в отладочных сборках, и имеет значение true, если диалоговое окно является модальным.|

## <a name="remarks"></a>Комментарии

`CAxDialogImpl` позволяет создать модальное или немодальное диалоговое окно. `CAxDialogImpl` предоставляет процедуру диалогового окна, которая использует схему сообщений по умолчанию для направления сообщений соответствующим обработчикам.

`CAxDialogImpl` является производным от `CDialogImplBaseT` , который, в свою очередь, является производным от *тбасе* (по умолчанию `CWindow` ) и `CMessageMap` .

Класс должен определять элемент Идд, указывающий идентификатор ресурса шаблона диалогового окна. Например, при добавлении объекта диалогового окна ATL с помощью диалогового окна **Добавление класса** в класс автоматически добавляется следующая строка:

[!code-cpp[NVC_ATL_Windowing#41](../../atl/codesnippet/cpp/caxdialogimpl-class_1.h)]

где `MyDialog` — **короткое имя** , указанное в мастере диалогового окна ATL.

Дополнительные сведения см. [в разделе Реализация диалогового окна](../../atl/implementing-a-dialog-box.md) .

Обратите внимание, что элемент управления ActiveX в модальном диалоговом окне, созданном с помощью `CAxDialogImpl` , не поддерживает сочетания клавиш. Для поддержки сочетаний клавиш в диалоговом окне, созданном с помощью `CAxDialogImpl` , создайте немодальное диалоговое окно и с помощью собственного цикла обработки сообщений используйте [каксдиалогимпл:: исдиалогмессаже](#isdialogmessage) после получения сообщения из очереди для обработки сочетания клавиш.

Дополнительные сведения о см `CAxDialogImpl` . в разделе [часто задаваемые вопросы об элементе управления ATL](../../atl/atl-control-containment-faq.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[кмессажемап](../../atl/reference/cmessagemap-class.md)

`TBase`

`CWindowImplRoot`

`CDialogImplBaseT`

`CAxDialogImpl`

## <a name="requirements"></a>Требования

**Заголовок:** atlwin. h

## <a name="caxdialogimpladvisesinkmap"></a><a name="advisesinkmap"></a> Каксдиалогимпл:: Адвисесинкмап

Вызовите этот метод, чтобы рекомендовать или отменять все записи в сопоставлении событий в схеме приемника объекта.

```
HRESULT AdviseSinkMap(bool bAdvise);
```

### <a name="parameters"></a>Параметры

*бадвисе*<br/>
Задайте значение true, если должны быть рекомендованы все записи приемника. значение false, если все записи приемника должны быть нерекомендуемыми.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

## <a name="caxdialogimplcreate"></a><a name="create"></a> Каксдиалогимпл:: Create

Вызовите этот метод, чтобы создать немодальное диалоговое окно.

```
HWND Create(HWND hWndParent, LPARAM dwInitParam = NULL);
HWND Create(HWND hWndParent, RECT&, LPARAM dwInitParam = NULL);
```

### <a name="parameters"></a>Параметры

*хвндпарент*<br/>
окне Маркер окна владельца.

*двинитпарам*<br/>
окне Указывает значение, передаваемое в диалоговое окно в параметре *lParam* сообщения WM_INITDIALOG.

*&RECT*<br/>
Этот параметр не используется. Этот параметр передается методом `CComControl` .

### <a name="return-value"></a>Возвращаемое значение

Маркер для вновь созданного диалогового окна.

### <a name="remarks"></a>Комментарии

Это диалоговое окно автоматически прикрепляется к `CAxDialogImpl` объекту. Чтобы создать модальное диалоговое окно, вызовите [DoModal](#domodal).

Второе переопределение предоставляется только для того, чтобы в [ккомконтрол](../../atl/reference/ccomcontrol-class.md)можно было использовать диалоговые окна.

## <a name="caxdialogimpldestroywindow"></a><a name="destroywindow"></a> Каксдиалогимпл::D Естройвиндов

Вызовите этот метод, чтобы уничтожить немодальное диалоговое окно.

```
BOOL DestroyWindow();
```

### <a name="return-value"></a>Возвращаемое значение

Значение TRUE, если окно успешно удалено; в противном случае — FALSE.

### <a name="remarks"></a>Комментарии

Не вызывайте `DestroyWindow` для уничтожения модального диалогового окна. Вместо этого вызовите метод [EndDialog](#enddialog) .

## <a name="caxdialogimpldomodal"></a><a name="domodal"></a> Каксдиалогимпл::D Омодал

Вызовите этот метод, чтобы создать модальное диалоговое окно.

```
INT_PTR DoModal(
    HWND hWndParent = ::GetActiveWindow(),
    LPARAM dwInitParam = NULL);
```

### <a name="parameters"></a>Параметры

*хвндпарент*<br/>
окне Маркер окна владельца. Значение по умолчанию — возвращаемое значение функции Win32 [жетактивевиндов](/windows/win32/api/winuser/nf-winuser-getactivewindow) .

*двинитпарам*<br/>
окне Указывает значение, передаваемое в диалоговое окно в параметре *lParam* сообщения WM_INITDIALOG.

### <a name="return-value"></a>Возвращаемое значение

В случае успеха значение параметра *нреткоде* , указанное при вызове [EndDialog](#enddialog); в противном случае — значение-1.

### <a name="remarks"></a>Комментарии

Это диалоговое окно автоматически прикрепляется к `CAxDialogImpl` объекту.

Чтобы создать немодальное диалоговое окно, вызовите [CREATE](#create).

## <a name="caxdialogimplenddialog"></a><a name="enddialog"></a> Каксдиалогимпл:: EndDialog

Вызовите этот метод, чтобы уничтожить модальное диалоговое окно.

```
BOOL EndDialog(int nRetCode);
```

### <a name="parameters"></a>Параметры

*нреткоде*<br/>
окне Значение, возвращаемое функцией [DoModal](#domodal).

### <a name="return-value"></a>Возвращаемое значение

Значение TRUE, если диалоговое окно уничтожается; в противном случае — значение FALSE.

### <a name="remarks"></a>Комментарии

`EndDialog` метод должен вызываться с помощью процедуры диалогового окна. После уничтожения диалогового окна Windows использует значение *нреткоде* в качестве возвращаемого значения для `DoModal` , которое создало диалоговое окно.

> [!NOTE]
> Не вызывайте `EndDialog` для уничтожения немодального диалогового окна. Вместо этого вызовите [дестройвиндов](#destroywindow) .

## <a name="caxdialogimplgetdialogproc"></a><a name="getdialogproc"></a> Каксдиалогимпл:: Жетдиалогпрок

Вызовите этот метод, чтобы получить указатель на `DialogProc` функцию обратного вызова.

```
virtual DLGPROC GetDialogProc();
```

### <a name="return-value"></a>Возвращаемое значение

Возвращает указатель на `DialogProc` функцию обратного вызова.

### <a name="remarks"></a>Комментарии

`DialogProc`Функция является определяемой приложением функцией обратного вызова.

## <a name="caxdialogimplgetidd"></a><a name="getidd"></a> Каксдиалогимпл:: Жетидд

Вызовите этот метод, чтобы получить идентификатор ресурса шаблона диалогового окна.

```
int GetIDD();
```

### <a name="return-value"></a>Возвращаемое значение

Возвращает идентификатор ресурса шаблона диалогового окна.

## <a name="caxdialogimplisdialogmessage"></a><a name="isdialogmessage"></a> Каксдиалогимпл:: Исдиалогмессаже

Вызовите этот метод, чтобы определить, предназначено ли сообщение для этого диалогового окна, и, если это так, обработать сообщение.

```
BOOL IsDialogMessage(LPMSG pMsg);
```

### <a name="parameters"></a>Параметры

*пмсг*<br/>
Указатель на структуру [MSG](/windows/win32/api/winuser/ns-winuser-msg) , содержащую сообщение для проверки.

### <a name="return-value"></a>Возвращаемое значение

Возвращает значение TRUE, если сообщение было обработано; в противном случае — значение FALSE.

### <a name="remarks"></a>Комментарии

Этот метод предназначен для вызова в цикле обработки сообщений.

## <a name="caxdialogimplm_bmodal"></a><a name="m_bmodal"></a> Каксдиалогимпл:: m_bModal

Переменная, которая существует только в отладочных сборках, и имеет значение true, если диалоговое окно является модальным.

```
bool m_bModal;
```

## <a name="see-also"></a>См. также раздел

[Класс CDialogImpl](../../atl/reference/cdialogimpl-class.md)<br/>
[Общие сведения о классах](../../atl/atl-class-overview.md)
