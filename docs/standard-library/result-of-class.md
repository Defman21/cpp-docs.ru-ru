---
description: 'Дополнительные сведения о: result_of классе'
title: Класс result_of
ms.date: 02/21/2019
f1_keywords:
- type_traits/std::result_of
- type_traits/std::result_of_t
- type_traits/std::result_of::type
helpviewer_keywords:
- std::result_of
- std::result_of_t
- std::result_of::type
ms.assetid: 5374a096-4b4a-4712-aa97-6852c5cdd6be
ms.openlocfilehash: 2aba6b073309be064b9ff0edc7bffa4d8d0098e7
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97273908"
---
# <a name="result_of-class"></a>Класс result_of

Определяет возвращаемый тип вызываемого типа, который принимает заданные типы аргументов. Добавлено в C++ 14, не рекомендуется в C++ 17.

## <a name="syntax"></a>Синтаксис

```cpp
template<class>
struct result_of; // Causes a static assert

template <class Fn, class... ArgTypes>
struct result_of<Fn(ArgTypes...)>;

// Helper type
template<class T>
   using result_of_t = typename result_of<T>::type;
```

### <a name="parameters"></a>Параметры

*FN*\
Вызываемый тип для запроса.

*аргтипес*\
Типы списка аргументов к вызываемому типу для запроса.

## <a name="remarks"></a>Комментарии

Используйте этот шаблон для определения во время компиляции типа результата `Fn` ( `ArgTypes` ), где *fn* — это вызываемый тип, ссылка на функцию или ссылка на вызываемый тип, вызываемая с помощью списка аргументов типов в *аргтипес*. `type`Член шаблона класса называет тип результата, `decltype(std::invoke(declval<Fn>(), declval<ArgTypes>()...))` Если неоцененное выражение `std::invoke(declval<Fn>(), declval<ArgTypes>()...)` имеет правильный формат. В противном случае шаблон класса не имеет члена `type` . Тип *fn* и все типы в пакете параметров *аргтипес* должны быть полными типами, **`void`** или массивами с неизвестной границей. Не рекомендуется в пользу [invoke_result](invoke-result-class.md) в c++ 17.

## <a name="requirements"></a>Требования

**Заголовок:**\<type_traits>

**Пространство имен:** std

## <a name="see-also"></a>См. также раздел

[<type_traits>](../standard-library/type-traits.md)\
[Класс invoke_result](invoke-result-class.md)
