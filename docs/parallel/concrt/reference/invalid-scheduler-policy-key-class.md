---
description: 'Дополнительные сведения о: invalid_scheduler_policy_key классе'
title: Класс invalid_scheduler_policy_key
ms.date: 11/04/2016
f1_keywords:
- invalid_scheduler_policy_key
- CONCRT/concurrency::invalid_scheduler_policy_key
- CONCRT/concurrency::invalid_scheduler_policy_key::invalid_scheduler_policy_key
helpviewer_keywords:
- invalid_scheduler_policy_key class
ms.assetid: 6a7c42fe-9bc4-4a02-bebb-99fe9ef9817d
ms.openlocfilehash: d352246cf0fe94f0ba5ee567f353680c89efcddc
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97334510"
---
# <a name="invalid_scheduler_policy_key-class"></a>Класс invalid_scheduler_policy_key

Этот класс описывает исключение, создаваемое, когда конструктору объекта `SchedulerPolicy` передается неверный или неизвестный ключ или методу `SetPolicyValue` объекта `SchedulerPolicy` передается ключ, который должен быть изменен другими средствами, такими как метод `SetConcurrencyLimits`.

## <a name="syntax"></a>Синтаксис

```cpp
class invalid_scheduler_policy_key : public std::exception;
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[invalid_scheduler_policy_key](#ctor)|Перегружен. Создает объект `invalid_scheduler_policy_key`.|

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`exception`

`invalid_scheduler_policy_key`

## <a name="requirements"></a>Требования

**Заголовок:** ConcRT. h

**Пространство имен:** параллелизм

## <a name="invalid_scheduler_policy_key"></a><a name="ctor"></a> invalid_scheduler_policy_key

Создает объект `invalid_scheduler_policy_key`.

```cpp
explicit _CRTIMP invalid_scheduler_policy_key(_In_z_ const char* _Message) throw();

invalid_scheduler_policy_key() throw();
```

### <a name="parameters"></a>Параметры

*_Message*<br/>
Описательное сообщение об ошибке.

## <a name="see-also"></a>См. также раздел

[Пространство имен Concurrency](concurrency-namespace.md)<br/>
[Класс SchedulerPolicy](schedulerpolicy-class.md)
