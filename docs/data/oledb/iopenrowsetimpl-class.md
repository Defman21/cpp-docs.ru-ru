---
description: 'Дополнительные сведения о: IOpenRowsetImpl Class'
title: Класс IOpenRowsetImpl
ms.date: 11/04/2016
f1_keywords:
- IOpenRowsetImpl
- IOpenRowsetImpl.CreateRowset
- IOpenRowsetImpl::CreateRowset
- OpenRowset
- IOpenRowsetImpl::OpenRowset
- IOpenRowsetImpl.OpenRowset
helpviewer_keywords:
- IOpenRowsetImpl class
- CreateRowset method
- OpenRowset method
ms.assetid: d259cedc-1db4-41cf-bc9f-5030907ab486
ms.openlocfilehash: 4ec7f8ebdab132854172f7e5f4dff7387e46717f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97317432"
---
# <a name="iopenrowsetimpl-class"></a>Класс IOpenRowsetImpl

Предоставляет реализацию `IOpenRowset` интерфейса.

## <a name="syntax"></a>Синтаксис

```cpp
template <class SessionClass>
class IOpenRowsetImpl : public IOpenRowset
```

### <a name="parameters"></a>Параметры

*сессионкласс*<br/>
Класс, производный от `IOpenRowsetImpl` .

## <a name="requirements"></a>Требования

**Заголовок:** atldb.h

## <a name="members"></a>Элементы

### <a name="methods"></a>Методы

| Имя | Описание |
|-|-|
|[CreateRowset](#createrowset)|Создает объект набора строк. Не вызывается непосредственно пользователем.|
|[BULK](#openrowset)|Открывает и возвращает набор строк, включающий все строки из одной базовой таблицы или индекса. (Не в ATLDB. Высоты|

## <a name="remarks"></a>Комментарии

Интерфейс [IOpenRowset](/previous-versions/windows/desktop/ms716946(v=vs.85)) является обязательным для объекта сеанса. Он открывает и возвращает набор строк, включающий все строки из одной базовой таблицы или индекса.

## <a name="iopenrowsetimplcreaterowset"></a><a name="createrowset"></a> IOpenRowsetImpl:: CreateRowset

Создает объект набора строк. Не вызывается непосредственно пользователем. См. раздел [IOpenRowset:: OPENROWSET](/previous-versions/windows/desktop/ms716724(v=vs.85)) в *справочнике программиста OLE DB.*

### <a name="syntax"></a>Синтаксис

```cpp
template template <class RowsetClass>
HRESULT CreateRowset(IUnknown* pUnkOuter,
   DBID* pTableID,
   DBID* pIndexID,
   REFIID riid,
   ULONG cPropertySets,
   DBPROPSET rgPropertySets[],
   IUnknown** ppRowset,
   RowsetClass*& pRowsetObj);
```

#### <a name="parameters"></a>Параметры

*RowsetClass*<br/>
Член класса шаблона, представляющий класс набора строк пользователя. Обычно создается мастером.

*провсетобж*<br/>
заполняет Указатель на объект набора строк. Обычно этот параметр не используется, но его можно использовать, если необходимо выполнить больше работы над набором строк перед передачей его в COM-объект. Время существования *провсетобж* привязывается *ппровсет*.

Другие параметры см. в разделе [IOpenRowset:: OPENROWSET](/previous-versions/windows/desktop/ms716724(v=vs.85)) в *справочнике программиста OLE DB.*

## <a name="iopenrowsetimplopenrowset"></a><a name="openrowset"></a> IOpenRowsetImpl:: OpenRowset

Открывает и возвращает набор строк, включающий все строки из одной базовой таблицы или индекса.

### <a name="syntax"></a>Синтаксис

```cpp
HRESULT OpenRowset(IUnknown* pUnkOuter,
   DBID* pTableID,
   DBID* pIndexID,
   REFIID riid,
   ULONG cPropertySets,
   DBPROPSET rgPropertySets[],
   IUnknown** ppRowset);
```

#### <a name="parameters"></a>Параметры

См. раздел [IOpenRowset:: OPENROWSET](/previous-versions/windows/desktop/ms716724(v=vs.85)) в *справочнике программиста OLE DB*.

### <a name="remarks"></a>Комментарии

Этот метод не найден в ATLDB. H. Он создается мастером объектов ATL при создании поставщика.

## <a name="see-also"></a>См. также раздел

[Шаблоны поставщика OLE DB](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[Архитектура шаблона поставщика OLE DB](../../data/oledb/ole-db-provider-template-architecture.md)
