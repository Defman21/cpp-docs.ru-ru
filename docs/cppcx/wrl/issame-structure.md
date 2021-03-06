---
description: 'Подробнее: та же структура'
title: IsSame - структура
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- internal/Microsoft::WRL::Details::IsSame
- internal/Microsoft::WRL::Details::IsSame::value
helpviewer_keywords:
- Microsoft::WRL::Details::IsSame structure
- Microsoft::WRL::Details::IsSame::value constant
ms.assetid: 1eddbc3f-3cc5-434f-8495-e4477e1f868e
ms.openlocfilehash: b00e85f55fc80af2dd00dc20f090a7b18678f579
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97298933"
---
# <a name="issame-structure"></a>IsSame - структура

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

## <a name="syntax"></a>Синтаксис

```cpp
template <typename T1, typename T2>
struct IsSame;

template <typename T1>
struct IsSame<T1, T1>;
```

### <a name="parameters"></a>Параметры

*T1*<br/>
Тип.

*T2*<br/>
Другой тип.

## <a name="remarks"></a>Комментарии

Определяет, совпадают ли указанные типы друг с другом.

## <a name="members"></a>Элементы

### <a name="public-constants"></a>Открытые константы

Имя                    | Описание
----------------------- | --------------------------------------------------
[То же:: значение](#value) | Указывает, совпадают ли заданные типы друг с другом.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`IsSame`

## <a name="requirements"></a>Требования

**Заголовок:** internal. h

**Пространство имен:** Microsoft:: WRL::D состояния

## <a name="issamevalue"></a><a name="value"></a> То же:: значение

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

```cpp
template <typename T1, typename T2>
struct IsSame
{
    static const bool value = false;
};

template <typename T1>
struct IsSame<T1, T1>
{
    static const bool value = true;
};
```

### <a name="remarks"></a>Комментарии

Указывает, совпадают ли заданные типы друг с другом.

`value` имеет значение **`true`** , если параметры шаблона одинаковы, и **`false`** Если параметры шаблона отличаются.
