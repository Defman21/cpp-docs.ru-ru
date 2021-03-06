---
description: Дополнительные сведения о классе норм.
title: Класс norm
ms.date: 11/04/2016
f1_keywords:
- AMP_SHORT_VECTORS/norm
- AMP_SHORT_VECTORS/Concurrency::graphics::norm Constructor
ms.assetid: 73002f3d-c25e-4119-bcd3-4c46c9b6abf1
ms.openlocfilehash: 29e376e5e42212c87ae244c7a606a38d6a07ddf1
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97327648"
---
# <a name="norm-class"></a>Класс norm

Представляет значение нормы. Каждый элемент является числом с плавающей запятой в диапазоне [-1.0 f, 1.0 f].

## <a name="syntax"></a>Синтаксис

```cpp
class norm;
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[норма, конструктор](#ctor)|Перегружен. Конструктор по умолчанию. Инициализируйте до 0,0 f.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Описание|
|----------|-----------------|
|норма:: operator-||
|норма:: operator--||
|норма:: оператор float|Оператор преобразования. Преобразуйте нормативное число в значение с плавающей запятой.|
|норма:: operator * =||
|норма:: оператор/=||
|норма:: operator + +||
|норма:: operator + =||
|норма:: оператор =||
|норма:: operator-=||

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`norm`

## <a name="requirements"></a>Требования

**Заголовок:** amp_short_vectors. h

**Пространство имен:** Concurrency:: Graphics

## <a name="norm"></a><a name="ctor"></a> норма

Конструктор по умолчанию. Инициализируйте до 0,0 f.

```cpp
norm(
    void) restrict(amp,
    cpu);

explicit norm(
    float _V) restrict(amp,
    cpu);

explicit norm(
    unsigned int _V) restrict(amp,
    cpu);

explicit norm(
    int _V) restrict(amp,
    cpu);

explicit norm(
    double _V) restrict(amp,
    cpu);

norm(
    const norm& _Other) restrict(amp,
    cpu);

norm(
    const unorm& _Other) restrict(amp,
    cpu);
```

### <a name="parameters"></a>Параметры

*_V*<br/>
Значение, используемое для инициализации.

*_Other*<br/>
Объект, используемый для инициализации.

## <a name="see-also"></a>См. также раздел

[Пространство имен Concurrency::graphics](concurrency-graphics-namespace.md)
