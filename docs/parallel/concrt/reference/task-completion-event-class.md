---
description: 'Дополнительные сведения о: task_completion_event классе'
title: Класс task_completion_event
ms.date: 11/04/2016
f1_keywords:
- task_completion_event
- PPLTASKS/concurrency::task_completion_event
- PPLTASKS/concurrency::task_completion_event::task_completion_event
- PPLTASKS/concurrency::task_completion_event::set
- PPLTASKS/concurrency::task_completion_event::set_exception
helpviewer_keywords:
- task_completion_event class
ms.assetid: fb19ed98-f245-48dc-9ba5-487ba879b28a
ms.openlocfilehash: 791b68d6a67ea2f8a9697b69266e8744455f845c
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97188369"
---
# <a name="task_completion_event-class"></a>Класс task_completion_event

Класс `task_completion_event` позволяет отложить выполнение задачи до выполнения условия или запустить задачу в ответ на внешнее событие.

## <a name="syntax"></a>Синтаксис

```cpp
template<typename _ResultType>
class task_completion_event;

template<>
class task_completion_event<void>;
```

### <a name="parameters"></a>Параметры

*_ResultType*<br/>
Тип результата данного класса `task_completion_event`.

## <a name="members"></a>Элементы

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[task_completion_event](#ctor)|Формирует объект `task_completion_event`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[set](#set)|Перегружен. Задает событие завершения задачи.|
|[set_exception](#set_exception)|Перегружен. Распространяет исключение для всех задач, связанных с этим событием.|

## <a name="remarks"></a>Комментарии

Если требуется создать задачу, которая будет завершена и, тем самым, будет иметь запланированное продолжение для выполнения в определенный момент в будущем, следует использовать задачу, созданную из события завершения задачи. Объект `task_completion_event` должен быть того же типа, что и создаваемая задача. Вызов метода set для события завершения задачи со значением такого типа приведет к завершению соответствующей задачи и предоставит это значение как результат продолжения.

Если о событии завершения задачи не сообщается, все задачи, созданные из этого события, будут отменены при его уничтожении.

`task_completion_event` ведет себя как интеллектуальный указатель и должен передаваться по значению.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`task_completion_event`

## <a name="requirements"></a>Требования

**Заголовок:** из ppltasks. h

**Пространство имен:** параллелизм

## <a name="set"></a><a name="set"></a> параметр

Задает событие завершения задачи.

```cpp
bool set(_ResultType _Result) const ;

bool set() const ;
```

### <a name="parameters"></a>Параметры

*_Result*<br/>
Результат для задания этого события в.

### <a name="return-value"></a>Возвращаемое значение

Метод возвращает значение, **`true`** если оно было успешным при установке события. Он возвращает **`false`** значение, если событие уже задано.

### <a name="remarks"></a>Комментарии

При наличии нескольких или одновременных вызовов метод `set` будет успешно выполнен только при первом вызове, а его результат (если таковой имеется) будет сохранен в событии завершения задачи. Остальные наборы игнорируются, и метод возвратит значение false. При задании события завершения задачи все задачи, созданные из этого события, будут немедленно завершены и будут планироваться его продолжения (при наличии). Объекты завершения задач, которые имеют `_ResultType` значение, отличное от, **`void`** передаст значения их продолжений.

## <a name="set_exception"></a><a name="set_exception"></a> set_exception

Распространяет исключение для всех задач, связанных с этим событием.

```cpp
template<typename _E>
__declspec(noinline) bool set_exception(_E _Except) const;

__declspec(noinline) bool set_exception(std::exception_ptr _ExceptionPtr) const ;
```

### <a name="parameters"></a>Параметры

*_E*<br/>
Тип исключения.

*_Except*<br/>
Заданное исключение.

*_ExceptionPtr*<br/>
Указатель на исключение для установки.

### <a name="return-value"></a>Возвращаемое значение

## <a name="task_completion_event"></a><a name="ctor"></a> task_completion_event

Формирует объект `task_completion_event`.

```cpp
task_completion_event();
```

## <a name="see-also"></a>См. также раздел

[Пространство имен Concurrency](concurrency-namespace.md)
