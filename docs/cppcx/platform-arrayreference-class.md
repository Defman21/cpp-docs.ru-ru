---
description: 'Дополнительные сведения о классе Platform:: ArrayReference'
title: Класс Platform::ArrayReference
ms.date: 10/16/2019
ms.topic: reference
f1_keywords:
- VCCORLIB/Platform::ArrayReference::ArrayReference
helpviewer_keywords:
- Platform::ArrayReference Class
ms.assetid: 9ab3b15e-8a60-4600-8fcb-7d6c86284f4b
ms.openlocfilehash: 6d883dd369b4b439bd02a337017e8c13731999d0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97284087"
---
# <a name="platformarrayreference-class"></a>Класс Platform::ArrayReference

`ArrayReference` — тип оптимизации, который можно заменить на [Platform::Array^](../cppcx/platform-array-class.md) во входных параметрах, если требуется заполнить входными данными массив в стиле языка C.

## <a name="syntax"></a>Синтаксис

```cpp
class ArrayReference
```

### <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[ArrayReference:: ArrayReference](#ctor)|Инициализирует новый экземпляр класса `ArrayReference`.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Описание|
|----------|-----------------|
|[Оператор ArrayReference:: operator ()](#operator-call)|Преобразует этот объект `ArrayReference` в `Platform::Array<T>^*`.|
|[Оператор ArrayReference::operator=](#operator-assign)|Назначает содержимое другой ссылки `ArrayReference` этому экземпляру.|

## <a name="exceptions"></a>Исключения

### <a name="remarks"></a>Remarks

Использование `ArrayReference` для заполнения массива в стиле языка C позволяет избежать дополнительной операции копирования, которая потребовалось бы при копировании сначала в переменную `Platform::Array` , а затем в массив в стиле языка C. При использовании `ArrayReference`выполняется только одна операция копирования. Пример кода см. в разделе [Array и WriteOnlyArray](../cppcx/array-and-writeonlyarray-c-cx.md).

### <a name="requirements"></a>Требования

**Минимальный поддерживаемый клиент:** Windows 8

**Минимальный поддерживаемый сервер:** Windows Server 2012

**Пространство имен:** Platform

**Заголовок:** vccorlib.h

## <a name="arrayreferencearrayreference-constructor"></a><a name="ctor"></a> Конструктор ArrayReference:: ArrayReference

Инициализирует новый экземпляр класса [Platform:: ArrayReference](../cppcx/platform-arrayreference-class.md) .

### <a name="syntax"></a>Синтаксис

```cpp
ArrayReference(TArg* ataArg, unsigned int sizeArg, bool needsInitArg = false);
ArrayReference(ArrayReference&& otherArg)
```

### <a name="parameters"></a>Параметры

*датаарг*<br/>
Указатель на данные массива.

*сизеарг*<br/>
Количество элементов в исходном массиве.

*осерарг*<br/>
Объект `ArrayReference`, данные которого будут перемещены для инициализации нового экземпляра.

### <a name="remarks"></a>Комментарии

## <a name="arrayreferenceoperator-operator"></a><a name="operator-assign"></a> Оператор ArrayReference:: operator =

Присваивает указанный объект текущему объекту [Platform:: ArrayReference](../cppcx/platform-arrayreference-class.md) с помощью семантики перемещения.

### <a name="syntax"></a>Синтаксис

```cpp
ArrayReference& operator=(ArrayReference&& otherArg);
```

### <a name="parameters"></a>Параметры

*осерарг*<br/>
Присваивает перемещенный объект текущему объекту `ArrayReference`.

### <a name="return-value"></a>Возвращаемое значение

Ссылка на объект типа `ArrayReference`.

### <a name="remarks"></a>Комментарии

`Platform::ArrayReference` — это стандартный шаблон класса C++, а не ссылочный класс.

## <a name="arrayreferenceoperator-operator"></a><a name="operator-call"></a> Оператор ArrayReference:: operator ()

Преобразует текущий объект [Platform:: ArrayReference](../cppcx/platform-arrayreference-class.md) обратно в класс [Platform:: Array](../cppcx/platform-array-class.md) .

### <a name="syntax"></a>Синтаксис

```cpp
Array<TArg>^ operator ();
```

### <a name="return-value"></a>Возвращаемое значение

Дескриптор для объекта типа `Array<TArg>^`

### <a name="remarks"></a>Комментарии

[Platform:: ArrayReference](../cppcx/platform-arrayreference-class.md) является стандартным шаблоном класса C++, а [Platform:: Array](../cppcx/platform-array-class.md) — ссылочным классом.

## <a name="see-also"></a>См. также раздел

[Пространство имен Platform](../cppcx/platform-namespace-c-cx.md)
