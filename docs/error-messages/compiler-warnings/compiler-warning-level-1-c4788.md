---
description: 'Дополнительные сведения: предупреждение компилятора (уровень 1) C4788'
title: Предупреждение компилятора (уровень 1) C4788
ms.date: 11/04/2016
f1_keywords:
- C4788
helpviewer_keywords:
- C4788
ms.assetid: 47d75bda-f833-4bdd-93a0-a134df0cd303
ms.openlocfilehash: 2aa87fd8a09b9f308e7fbb51fc4f05792210b0c1
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97234609"
---
# <a name="compiler-warning-level-1-c4788"></a>Предупреждение компилятора (уровень 1) C4788

"идентификатор": идентификатор был усечен до "числа" символов

Компилятор ограничивает максимально допустимую длину имени функции. Когда компилятор создает функлетс для кода EH/SEH, он формирует имя Библиотека funclet, добавляя перед именем функции некоторый текст, например "__catch", " \_ _unwind" или другую строку.

Полученное имя Библиотека funclet может быть слишком длинным, а компилятор усекает его и создаст C4788.

Чтобы устранить это предупреждение, сократите исходное имя функции. Если функция является функцией или методом шаблона C++, используйте typedef для части имени. Пример:

```cpp
C1<x, y, z<T>>::C2<a,b,c>::f
```

можно заменить на:

```cpp
typedef C1<x, y, z<T>>::C2<a,b,c> new_class ;
new_class::f
```

Это предупреждение возникает только в компиляторе x64.
