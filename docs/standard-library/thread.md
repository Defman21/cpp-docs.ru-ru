---
description: 'Дополнительные сведения: &lt; Thread&gt;'
title: '&lt;thread&gt;'
ms.date: 11/04/2016
f1_keywords:
- <thread>
ms.assetid: 0c858405-4efb-449d-bf76-70d3693c9234
ms.openlocfilehash: 3387d96772f1ed3322ce79b744e17b6bf494140d
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97289625"
---
# <a name="ltthreadgt"></a>&lt;thread&gt;

Включите стандартный заголовок \<thread> для определения класса `thread` и различных вспомогательных функций.

## <a name="syntax"></a>Синтаксис

```cpp
#include <thread>
```

## <a name="remarks"></a>Remarks

> [!NOTE]
> В коде, компилируемом с помощью **/CLR**, этот заголовок блокируется.

`__STDCPP_THREADS__`Макрос определяется как ненулевое значение, чтобы указать, что потоки поддерживаются этим заголовком.

## <a name="members"></a>Элементы

### <a name="public-classes"></a>Открытые классы

|Имя|Описание|
|----------|-----------------|
|[Класс Thread](../standard-library/thread-class.md)|Определяет объект, используемый для наблюдения за потоком выполнения в приложении и управления им.|

### <a name="public-structures"></a>Открытые структуры

|Имя|Описание|
|----------|-----------------|
|[Структура hash (Стандартная библиотека C++)](../standard-library/hash-structure-stl.md)|Определяет функцию-член, которая возвращает значение, которое однозначно определяется объектом `thread::id` . Функция-член определяет функцию [хэширования](../standard-library/hash-class.md) , которая подходит для сопоставления значений типа `thread::id` с распределением значений индекса.|

### <a name="public-functions"></a>Открытые функции

|Имя|Описание|
|----------|-----------------|
|[get_id](../standard-library/thread-functions.md#get_id)|Уникально идентифицирует текущий поток выполнения.|
|[sleep_for](../standard-library/thread-functions.md#sleep_for)|Блокирует вызывающий поток.|
|[sleep_until](../standard-library/thread-functions.md#sleep_until)|Блокирует вызывающий поток по крайней мере до указанного времени.|
|[позиции](../standard-library/thread-functions.md#swap)|Обменивается состояниями двух `thread` объектов.|
|[yield](../standard-library/thread-functions.md#yield)|Сигнализирует операционной системе, что необходимо запустить другие потоки, даже если в обычной ситуации текущий поток продолжал бы выполняться.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Описание|
|----------|-----------------|
|[Оператор>=](../standard-library/thread-operators.md#op_gt_eq)|Определяет, справедливо ли, что один из объектов `thread::id` больше другого или равен ему.|
|[Оператор> оператора](../standard-library/thread-operators.md#op_gt)|Определяет, справедливо ли, что один из объектов `thread::id` больше другого или равен ему.|
|[Оператор<=](../standard-library/thread-operators.md#op_lt_eq)|Определяет, справедливо ли, что один из объектов `thread::id` меньше другого или равен ему.|
|[Оператор< оператора](../standard-library/thread-operators.md#op_lt)|Определяет, справедливо ли, что один объект `thread::id` меньше другого.|
|[оператор operator! =](../standard-library/thread-operators.md#op_neq)|Проверяет неравенство двух объектов `thread::id`.|
|[оператор operator = =](../standard-library/thread-operators.md#op_eq_eq)|Сравнивает два объекта `thread::id` на равенство.|
|[Оператор<< оператора](../standard-library/thread-operators.md#op_lt_lt)|Вставляет текстовое представление объекта `thread::id` в поток.|

## <a name="see-also"></a>См. также раздел

[Справочник по файлам заголовков](../standard-library/cpp-standard-library-header-files.md)\
[Безопасность потоков в стандартной библиотеке C++](../standard-library/thread-safety-in-the-cpp-standard-library.md)
