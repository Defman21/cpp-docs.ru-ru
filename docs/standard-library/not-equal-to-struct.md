---
description: 'Дополнительные сведения о: not_equal_to struct'
title: not_equal_to - структура
ms.date: 11/04/2016
f1_keywords:
- functional/std::not_equal_to
helpviewer_keywords:
- not_equal_to function
- not_equal_to struct
ms.assetid: 333fce09-4f51-44e0-ba26-533bccffd485
ms.openlocfilehash: fabcfe2df6f0e4676d558eb9f7c47e1e9c356d62
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97338126"
---
# <a name="not_equal_to-struct"></a>not_equal_to - структура

Бинарный предикат, который выполняет операцию неравенства ( `operator!=` ) в своих аргументах.

## <a name="syntax"></a>Синтаксис

```
template <class Type = void>
struct not_equal_to : public binary_function<Type, Type, bool>
{
    bool operator()(const Type& Left, const Type& Right) const;
};

// specialized transparent functor for operator!=
template <>
struct not_equal_to<void>
{
  template <class T, class U>
  auto operator()(T&& Left, U&& Right) const`
    -> decltype(std::forward<T>(Left) != std::forward<U>(Right));
};
```

### <a name="parameters"></a>Параметры

*Тип*, *T*, *U*\
Любой тип, поддерживающий `operator!=`, принимающий операнды указанного или выводимого типа.

*Слева*\
Левый операнд в операции неравенства. Неспециализированный шаблон принимает ссылочный аргумент lvalue типа *Type*. Специализированный шаблон выполняет точную пересылку ссылочных аргументов lvalue и rvalue для выводимого типа *T*.

*Правильно*\
Правый операнд в операции неравенства. Неспециализированный шаблон принимает ссылочный аргумент lvalue типа *Type*. Специализированный шаблон выполняет точную пересылку ссылочных аргументов lvalue и rvalue для выводимого типа *U*.

## <a name="return-value"></a>Возвращаемое значение

Результат `Left != Right`. Специализированный шаблон выполняет точную пересылку результата типа, возвращаемого `operator!=`.

## <a name="remarks"></a>Комментарии

Объекты *типа должны быть* сравнимы по равенству. Для этого нужно, чтобы `operator!=`, определенный в наборе объектов, удовлетворял математическим свойствам отношения эквивалентности. Этим требованиям удовлетворяют все встроенные числовые типы и типы указателей.

## <a name="example"></a>Пример

```cpp
// functional_not_equal_to.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

int main( )
{
   vector <double> v1, v2, v3 (6);
   vector <double>::iterator Iter1, Iter2, Iter3;

   int i;
   for ( i = 0 ; i <= 5 ; i+=2 )
   {
      v1.push_back( 2.0 *i );
      v1.push_back( 2.0 * i + 1.0 );
   }

   int j;
   for ( j = 0 ; j <= 5 ; j+=2 )
   {
      v2.push_back( - 2.0 * j );
      v2.push_back( 2.0 * j + 1.0 );
   }

   cout << "The vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   cout << "The vector v2 = ( " ;
   for ( Iter2 = v2.begin( ) ; Iter2 != v2.end( ) ; Iter2++ )
      cout << *Iter2 << " ";
   cout << ")" << endl;

   // Testing for the element-wise equality between v1 & v2
   transform ( v1.begin( ), v1.end( ), v2.begin( ), v3.begin ( ),
      not_equal_to<double>( ) );

   cout << "The result of the element-wise not_equal_to comparsion\n"
      << "between v1 & v2 is: ( " ;
   for ( Iter3 = v3.begin( ) ; Iter3 != v3.end( ) ; Iter3++ )
      cout << *Iter3 << " ";
   cout << ")" << endl;
}
```

```Output
The vector v1 = ( 0 1 4 5 8 9 )
The vector v2 = ( -0 1 -4 5 -8 9 )
The result of the element-wise not_equal_to comparsion
between v1 & v2 is: ( 0 0 1 0 1 0 )
```
