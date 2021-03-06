---
description: 'Дополнительные сведения о: binary_function struct'
title: Структура binary_function
ms.date: 02/21/2019
f1_keywords:
- functional/std::binary_function
helpviewer_keywords:
- binary_function class
ms.assetid: 79b6d53d-644c-4add-b0ba-3a5f40f69c60
ms.openlocfilehash: 3a38579cc5026903dc7c3b7743afd81773b895b7
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97325549"
---
# <a name="binary_function-struct"></a>Структура binary_function

Пустая базовая структура, определяющая типы, которые могут наследоваться производными классами, предоставляющими объект бинарной функции. Не рекомендуется использовать в C++ 11, удалено в C++ 17.

## <a name="syntax"></a>Синтаксис

```cpp
struct binary_function {
   typedef Arg1 first_argument_type;
   typedef Arg2 second_argument_type;
   typedef Result result_type;
};
```

## <a name="remarks"></a>Remarks

Структура шаблона выступает в качестве основы для классов, в которых определяются функции-члены в виде:

> *result_type* * * operator () (const * * <em>first_argument_type</em> **&, const** <em>second_argument_type</em> **&) const**

Все такие бинарные функции могут ссылаться на тип своего первого аргумента как *first_argument_type*, тип второго аргумента как *second_argument_type* и возвращаемый тип как *result_type*.

## <a name="example"></a>Пример

```cpp
// functional_binary_function.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

template <class Type> class average:
binary_function<Type, Type, Type>
{
public:
   result_type operator( ) ( first_argument_type a,
                 second_argument_type b )
   {
      return (result_type) ( ( a + b ) / 2 );
   }
};

int main( )
{
   vector <double> v1, v2, v3 ( 6 );
   vector <double>::iterator Iter1, Iter2, Iter3;

   for ( int i = 1 ; i <= 6 ; i++ )
      v1.push_back( 11.0 / i );

   for ( int j = 0 ; j <= 5 ; j++ )
      v2.push_back( -2.0 * j );

   cout << "The vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   cout << "The vector v2 = ( " ;
   for ( Iter2 = v2.begin( ) ; Iter2 != v2.end( ) ; Iter2++ )
      cout << *Iter2 << " ";
   cout << ")" << endl;

   // Finding the element-wise averages of the elements of v1 & v2
   transform ( v1.begin( ),  v1.end( ), v2.begin( ), v3.begin ( ),
      average<double>( ) );

   cout << "The element-wise averages are: ( " ;
   for ( Iter3 = v3.begin( ) ; Iter3 != v3.end( ) ; Iter3++ )
      cout << *Iter3 << " ";
   cout << ")" << endl;
}
```

```Output
The vector v1 = ( 11 5.5 3.66667 2.75 2.2 1.83333 )
The vector v2 = ( -0 -2 -4 -6 -8 -10 )
The element-wise averages are: ( 5.5 1.75 -0.166667 -1.625 -2.9 -4.08333 )
```
