---
description: 'Дополнительные сведения о: Ошибка компилятора C2998'
title: Ошибка компилятора C2998
ms.date: 11/04/2016
f1_keywords:
- C2998
helpviewer_keywords:
- C2998
ms.assetid: 8193d491-b5d9-4477-acb1-cf166889c070
ms.openlocfilehash: 43370ee8659335f6d14a2850ba0b874434786ca0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97253615"
---
# <a name="compiler-error-c2998"></a>Ошибка компилятора C2998

"идентификатор": не может быть определением шаблона

Компилятору не удалось обработать синтаксис, используемый в определении шаблона.

Следующий пример приводит к возникновению ошибки C2998:

```cpp
// C2998.cpp
// compile with: /c
template <class T> int x = 1018; // C2998
```
