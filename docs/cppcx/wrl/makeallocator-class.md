---
description: 'Дополнительные сведения о: MakeAllocator Class'
title: MakeAllocator - класс
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- implements/Microsoft::WRL::Details::MakeAllocator
- implements/Microsoft::WRL::Details::MakeAllocator::Allocate
- implements/Microsoft::WRL::Details::MakeAllocator::Detach
- implements/Microsoft::WRL::Details::MakeAllocator::MakeAllocator
- implements/Microsoft::WRL::Details::MakeAllocator::~MakeAllocator
helpviewer_keywords:
- Microsoft::WRL::Details::MakeAllocator class
- Microsoft::WRL::Details::MakeAllocator::Allocate method
- Microsoft::WRL::Details::MakeAllocator::Detach method
- Microsoft::WRL::Details::MakeAllocator::MakeAllocator, constructor
- Microsoft::WRL::Details::MakeAllocator::~MakeAllocator, destructor
ms.assetid: a1114615-abd7-4a56-9bc3-750c118f0fa1
ms.openlocfilehash: c4e550dec37096a5ff6a41eccd4eb41968721a7d
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97344527"
---
# <a name="makeallocator-class"></a>MakeAllocator - класс

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

## <a name="syntax"></a>Синтаксис

```cpp
template<
    typename T,
    bool hasWeakReferenceSupport =
          !__is_base_of(RuntimeClassFlags<InhibitWeakReference>,
                        T)
>
class MakeAllocator;

template<typename T>
class MakeAllocator<T, false>;

template<typename T>
class MakeAllocator<T, true>;
```

### <a name="parameters"></a>Параметры

*T*<br/>
Имя типа.

*хасвеакреференцесуппорт*<br/>
**`true`** выделение памяти для объекта, который поддерживает слабые ссылки; **`false`** выделение памяти для объекта, который не поддерживает слабые ссылки.

## <a name="remarks"></a>Комментарии

Выделяет память для класса активируемого с поддержкой слабых ссылок или без нее.

Переопределите `MakeAllocator` класс для реализации модели выделения памяти, определяемой пользователем.

`MakeAllocator` обычно используется для предотвращения утечек памяти, если объект вызывается во время создания.

## <a name="members"></a>Элементы

### <a name="public-constructors"></a>Открытые конструкторы

name                                                  | Описание
----------------------------------------------------- | ----------------------------------------------------------------
[MakeAllocator:: MakeAllocator](#makeallocator)        | Инициализирует новый экземпляр класса `MakeAllocator`.
[MakeAllocator:: ~ MakeAllocator](#tilde-makeallocator) | Выполняет деинициализацию текущего экземпляра `MakeAllocator` класса.

### <a name="public-methods"></a>Открытые методы

name                                 | Описание
------------------------------------ | -----------------------------------------------------------------------------------------------------------
[MakeAllocator:: allocate](#allocate) | Выделяет память и связывает ее с текущим `MakeAllocator` объектом.
[MakeAllocator::D етач](#detach)     | Отменяет связь памяти, выделенной методом [выделения](#allocate) , из текущего `MakeAllocator` объекта.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`MakeAllocator`

## <a name="requirements"></a>Требования

**Заголовок:** Implements. h

**Пространство имен:** Microsoft:: WRL::D состояния

## <a name="makeallocatorallocate"></a><a name="allocate"></a> MakeAllocator:: allocate

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

```cpp
__forceinline void* Allocate();
```

### <a name="return-value"></a>Возвращаемое значение

В случае успеха указатель на выделенную память; в противном случае — **`nullptr`** .

### <a name="remarks"></a>Комментарии

Выделяет память и связывает ее с текущим `MakeAllocator` объектом.

Размер выделенной памяти — это размер типа, указанного в текущем `MakeAllocator` параметре шаблона.

Разработчику необходимо переопределить только `Allocate()` метод для реализации другой модели выделения памяти.

## <a name="makeallocatordetach"></a><a name="detach"></a> MakeAllocator::D етач

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

```cpp
__forceinline void Detach();
```

### <a name="remarks"></a>Комментарии

Отменяет связь памяти, выделенной методом [выделения](#allocate) , из текущего `MakeAllocator` объекта.

При вызове `Detach()` вы несете ответственность за удаление памяти, предоставленной `Allocate` методом.

## <a name="makeallocatormakeallocator"></a><a name="makeallocator"></a> MakeAllocator:: MakeAllocator

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

```cpp
MakeAllocator();
```

### <a name="remarks"></a>Комментарии

Инициализирует новый экземпляр класса `MakeAllocator`.

## <a name="makeallocatormakeallocator"></a><a name="tilde-makeallocator"></a> MakeAllocator:: ~ MakeAllocator

Поддерживает инфраструктуру WRL и не предназначен для непосредственного использования в коде.

```cpp
~MakeAllocator();
```

### <a name="remarks"></a>Комментарии

Выполняет деинициализацию текущего экземпляра `MakeAllocator` класса.

Этот деструктор также удаляет базовую выделенную память, если это необходимо.
