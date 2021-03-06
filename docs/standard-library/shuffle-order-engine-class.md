---
description: 'Дополнительные сведения о: shuffle_order_engine классе'
title: Класс shuffle_order_engine
ms.date: 11/04/2016
f1_keywords:
- random/std::shuffle_order_engine
- random/std::shuffle_order_engine::base
- random/std::shuffle_order_engine::discard
- random/std::shuffle_order_engine::operator()
- random/std::shuffle_order_engine::base_type
- random/std::shuffle_order_engine::seed
helpviewer_keywords:
- std::shuffle_order_engine [C++]
- std::shuffle_order_engine [C++], base
- std::shuffle_order_engine [C++], discard
- std::shuffle_order_engine [C++], base_type
- std::shuffle_order_engine [C++], seed
ms.assetid: 0bcd1fb0-44d7-4e59-bb1b-4a9b673a960d
ms.openlocfilehash: 3be8438ac0809d697d081d998450bde09d1d583e
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97154023"
---
# <a name="shuffle_order_engine-class"></a>Класс shuffle_order_engine

Создает случайную последовательность, изменяя порядок значений, возвращенных базовым механизмом.

## <a name="syntax"></a>Синтаксис

```cpp
template <class Engine, size_t K>
class shuffle_order_engine;
```

### <a name="parameters"></a>Параметры

*Ядре*\
Тип базового механизма.

*Занят*\
**Размер таблицы**. Количество элементов в буфере (таблице). **Предварительное условие**: `0 < K`

## <a name="members"></a>Элементы

`shuffle_order_engine::shuffle_order_engine`\
`shuffle_order_engine::base`\
`shuffle_order_engine::base_type`\
`shuffle_order_engine::discard`\
`shuffle_order_engine::operator()`\
`shuffle_order_engine::seed`

Дополнительные сведения о членах подсистемы см [\<random>](../standard-library/random.md) . в разделе.

## <a name="remarks"></a>Комментарии

Этот шаблон класса описывает *адаптер подсистемы* , который получает значения путем изменения порядка значений, возвращенных базовым механизмом. Каждый конструктор заполняет внутреннюю таблицу значениями *K* , возвращаемыми базовым механизмом, и при запросе значения выбирается случайный элемент из таблицы.

## <a name="requirements"></a>Требования

**Заголовок:**\<random>

**Пространство имен:** std

## <a name="see-also"></a>См. также раздел

[\<random>](../standard-library/random.md)
