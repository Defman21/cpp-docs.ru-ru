---
description: 'Дополнительные сведения о: отрицание структуры'
title: Структура negate
ms.date: 11/04/2016
f1_keywords:
- functional/std::negate
helpviewer_keywords:
- negate struct
- negate class
ms.assetid: 8a372686-786e-4262-b37c-ca13dc11e62f
ms.openlocfilehash: fccc583d38b797a856ed4e0915e5e0255bb9eaee
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97338235"
---
# <a name="negate-struct"></a>Структура negate

Стандартный объект функции, который выполняет над своим аргументом арифметическую операцию замены знака (унарное `operator-`).

## <a name="syntax"></a>Синтаксис

```
template <class Type = void>
struct negate : public unary_function<Type, Type>
{
    Type operator()(const Type& Left) const;
};

// specialized transparent functor for unary operator-
template <>
struct negate<void>
{
  template <class Type>
  auto operator()(Type&& Left) const`
    -> decltype(-std::forward<Type>(Left));
};
```

### <a name="parameters"></a>Параметры

*Тип*\
Любой тип, поддерживающий `operator-`, принимающий операнды указанного или выводимого типа.

*Слева*\
Операнд для замены знака. Специализированный шаблон выполняет точную пересылку ссылочных аргументов lvalue и rvalue для выводимого *типа*.

## <a name="return-value"></a>Возвращаемое значение

Результат `-Left`. Специализированный шаблон выполняет точную пересылку результата, который имеет тип, возвращаемый унарным методом `operator-` .

## <a name="example"></a>Пример

```cpp
// functional_negate.cpp
// compile with: /EHsc
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

int main( )
{
   vector <int> v1, v2 ( 8 );
   vector <int>::iterator Iter1, Iter2;

   int i;
   for ( i = -2 ; i <= 5 ; i++ )
   {
      v1.push_back( 5 * i );
   }

   cout << "The vector v1 = ( " ;
   for ( Iter1 = v1.begin( ) ; Iter1 != v1.end( ) ; Iter1++ )
      cout << *Iter1 << " ";
   cout << ")" << endl;

   // Finding the element-wise negatives of the vector v1
   transform ( v1.begin( ),  v1.end( ), v2.begin( ), negate<int>( ) );

   cout << "The negated elements of the vector = ( " ;
   for ( Iter2 = v2.begin( ) ; Iter2 != v2.end( ) ; Iter2++ )
      cout << *Iter2 << " ";
   cout << ")" << endl;
}
```

```Output
The vector v1 = ( -10 -5 0 5 10 15 20 25 )
The negated elements of the vector = ( 10 5 0 -5 -10 -15 -20 -25 )
```
