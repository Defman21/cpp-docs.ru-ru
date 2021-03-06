---
description: 'Дополнительные сведения о: CStreamRowset Class'
title: Класс CStreamRowset
ms.date: 11/04/2016
f1_keywords:
- ATL::CStreamRowset<TAccessor>
- ATL::CStreamRowset
- CStreamRowset
- ATL.CStreamRowset<TAccessor>
- ATL.CStreamRowset
- CStreamRowset::CStreamRowset
- CStreamRowset.CStreamRowset
- ATL.CStreamRowset.CStreamRowset
- ATL::CStreamRowset::CStreamRowset
- CStreamRowset<TAccessor>::CStreamRowset
- ATL::CStreamRowset<TAccessor>::CStreamRowset
- CStreamRowset<TAccessor>.Close
- ATL.CStreamRowset<TAccessor>.Close
- CStreamRowset::Close
- CStreamRowset<TAccessor>::Close
- ATL::CStreamRowset::Close
- ATL.CStreamRowset.Close
- ATL::CStreamRowset<TAccessor>::Close
- CStreamRowset.Close
helpviewer_keywords:
- CStreamRowset class
- CStreamRowset class, constructor
- Close method
ms.assetid: a106e953-a38a-464e-8ea5-28963d9e4811
ms.openlocfilehash: 278f85b36a2b4ec1c3d6b3c2bd5ecc5b47c5ef73
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97287818"
---
# <a name="cstreamrowset-class"></a>Класс CStreamRowset

Используется в `CCommand` `CTable` объявлении или.

## <a name="syntax"></a>Синтаксис

```cpp
template <class TAccessor = CAccessorBase>
class CStreamRowset
```

### <a name="parameters"></a>Параметры

*такцессор*<br/>
Класс метода доступа.

## <a name="requirements"></a>Требования

**Заголовок:** atldbcli.h

## <a name="members"></a>Элементы

### <a name="methods"></a>Методы

| Имя | Описание |
|-|-|
|[CStreamRowset](#cstreamrowset)|Конструктор. Создает и инициализирует `CStreamRowset` объект.|
|[Закрыть](#close)|Освобождает указатель интерфейса [ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85)) в классе.|

## <a name="remarks"></a>Комментарии

Используйте `CStreamRowset` в `CCommand` `CTable` объявлении или, например:

[!code-cpp[NVC_OLEDB_Consumer#11](../../data/oledb/codesnippet/cpp/cstreamrowset-class_1.cpp)]

или

[!code-cpp[NVC_OLEDB_Consumer#12](../../data/oledb/codesnippet/cpp/cstreamrowset-class_2.cpp)]

`ICommand::Execute` Возвращает `ISequentialStream` указатель, хранящийся в `m_spStream` . Затем используйте `Read` метод для получения данных (строки в Юникоде) в формате XML. Пример:

[!code-cpp[NVC_OLEDB_Consumer#13](../../data/oledb/codesnippet/cpp/cstreamrowset-class_3.cpp)]

SQL Server 2000 выполняет форматирование XML и будет возвращать все столбцы и все строки набора строк в виде одной строки XML.

> [!NOTE]
> Эта функция работает только с SQL Server 2000.

## <a name="cstreamrowsetcstreamrowset"></a><a name="cstreamrowset"></a> CStreamRowset:: CStreamRowset

Создает и инициализирует `CStreamRowset` объект.

### <a name="syntax"></a>Синтаксис

```cpp
CStreamRowset();
```

## <a name="cstreamrowsetclose"></a><a name="close"></a> CStreamRowset:: Close

Освобождает указатель интерфейса [ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85)) в классе.

### <a name="syntax"></a>Синтаксис

```cpp
void Close();
```

## <a name="see-also"></a>См. также раздел

[Шаблоны объекта-получателя OLE DB](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[Справочник по шаблонам потребителей OLE DB](../../data/oledb/ole-db-consumer-templates-reference.md)
