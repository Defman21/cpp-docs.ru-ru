---
description: 'Дополнительные сведения о: Кричедиткнтритем Class'
title: Класс Кричедиткнтритем
ms.date: 11/04/2016
f1_keywords:
- CRichEditCntrItem
- AFXRICH/CRichEditCntrItem
- AFXRICH/CRichEditCntrItem::CRichEditCntrItem
- AFXRICH/CRichEditCntrItem::SyncToRichEditObject
helpviewer_keywords:
- CRichEditCntrItem [MFC], CRichEditCntrItem
- CRichEditCntrItem [MFC], SyncToRichEditObject
ms.assetid: 6c0b4efe-0fb8-4621-b5e1-fdcb8ec48c3b
ms.openlocfilehash: 9e65e70a3fb03b65ebf9af7a619a5c4fbd3dba32
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97342964"
---
# <a name="cricheditcntritem-class"></a>Класс Кричедиткнтритем

С помощью [CRichEditView](../../mfc/reference/cricheditview-class.md) и [CRichEditDoc](../../mfc/reference/cricheditdoc-class.md)предоставляет функциональные возможности элемента управления Rich Edit в контексте архитектуры представления документов MFC.

## <a name="syntax"></a>Синтаксис

```
class CRichEditCntrItem : public COleClientItem
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[Кричедиткнтритем:: Кричедиткнтритем](#cricheditcntritem)|Формирует объект `CRichEditCntrItem`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Кричедиткнтритем:: Синкторичедитобжект](#synctoricheditobject)|Активирует элемент как другой тип.|

## <a name="remarks"></a>Комментарии

«Форматируемый элемент управления» — это окно, в котором пользователь может вводить и редактировать текст. Тексту можно присвоить форматирование символов и абзацев, а также включить внедренные объекты OLE. Элементы управления Rich Edit предоставляют программный интерфейс для форматирования текста. Однако приложение должно реализовывать любые компоненты пользовательского интерфейса, необходимые для того, чтобы сделать операции форматирования доступными для пользователя.

`CRichEditView` поддерживает текстовую характеристику текста и форматирования текста. `CRichEditDoc` поддерживает список элементов OLE клиента, которые находятся в представлении. `CRichEditCntrItem` предоставляет доступ на стороне контейнера к элементу OLE-клиента.

Этот общий элемент управления Windows (и, следовательно, [CRichEditCtrl](../../mfc/reference/cricheditctrl-class.md) и связанные классы) доступен только для программ, работающих под управлением Windows 95/98 и Windows NT версии 3,51 и более поздних версий.

Пример использования элементов контейнера с богатыми возможностями редактирования в приложении MFC см. в примере приложения [WordPad](../../overview/visual-cpp-samples.md) .

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CDocItem](../../mfc/reference/cdocitem-class.md)

[COleClientItem](../../mfc/reference/coleclientitem-class.md)

`CRichEditCntrItem`

## <a name="requirements"></a>Требования

**Заголовок:** афксрич. h

## <a name="cricheditcntritemcricheditcntritem"></a><a name="cricheditcntritem"></a> Кричедиткнтритем:: Кричедиткнтритем

Вызовите эту функцию, чтобы создать `CRichEditCntrItem` объект и добавить его в документ-контейнер.

```
CRichEditCntrItem(
    REOBJECT* preo = NULL,
    CRichEditDoc* pContainer = NULL);
```

### <a name="parameters"></a>Параметры

*прео*<br/>
Указатель на структуру [объекта](/windows/win32/api/richole/ns-richole-reobject) , описывающую элемент OLE. Новый `CRichEditCntrItem` объект создается вокруг этого объекта OLE. Если *прео* имеет значение null, то элемент клиента пуст.

*pContainer*<br/>
Указатель на документ контейнера, который будет содержать этот элемент. Если *pcontainer может* имеет значение null, необходимо явно вызвать [Коледокумент:: AddItem](../../mfc/reference/coledocument-class.md#additem) , чтобы добавить этот клиентский элемент в документ.

### <a name="remarks"></a>Комментарии

Эта функция не выполняет инициализацию OLE.

Дополнительные сведения см. в описании структуры [РЕобъектного объекта](/windows/win32/api/richole/ns-richole-reobject) в Windows SDK.

## <a name="cricheditcntritemsynctoricheditobject"></a><a name="synctoricheditobject"></a> Кричедиткнтритем:: Синкторичедитобжект

Вызовите эту функцию, чтобы синхронизировать аспект устройства, [дваспект](/windows/win32/api/wtypes/ne-wtypes-dvaspect), с `CRichEditCntrltem` указанным *Рео*.

```cpp
void SyncToRichEditObject(REOBJECT& reo);
```

### <a name="parameters"></a>Параметры

*рео*<br/>
Ссылка на структуру [объектов](/windows/win32/api/richole/ns-richole-reobject) , описывающую элемент OLE.

### <a name="remarks"></a>Комментарии

Дополнительные сведения см. в разделе [дваспект](/windows/win32/api/wtypes/ne-wtypes-dvaspect) в Windows SDK.

## <a name="see-also"></a>См. также раздел

[Образец WORDPAD для MFC](../../overview/visual-cpp-samples.md)<br/>
[Класс COleClientItem](../../mfc/reference/coleclientitem-class.md)<br/>
[Иерархическая диаграмма](../../mfc/hierarchy-chart.md)<br/>
[Класс CRichEditDoc](../../mfc/reference/cricheditdoc-class.md)<br/>
[Класс CRichEditView](../../mfc/reference/cricheditview-class.md)
