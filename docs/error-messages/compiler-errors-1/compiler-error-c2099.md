---
description: 'Дополнительные сведения о: Ошибка компилятора C2099'
title: Ошибка компилятора C2099
ms.date: 11/04/2016
f1_keywords:
- C2099
helpviewer_keywords:
- C2099
ms.assetid: 30e151ee-d458-4901-b0c0-d45054a913f5
ms.openlocfilehash: 03a021216bdb5228bb2ef9cba961b06161d20948
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97170273"
---
# <a name="compiler-error-c2099"></a>Ошибка компилятора C2099

инициализатор не является константой

Эта ошибка выдается только компилятором C и возникает только для неавтоматических переменных.  Компилятор инициализирует неавтоматические переменные при запуске программы, и значения, с которыми они инициализируются, должны быть константами.

## <a name="examples"></a>Примеры

Следующий пример приводит к возникновению ошибки C2099.

```c
// C2099.c
int j;
int *p;
j = *p;   // C2099 *p is not a constant
```

Ошибка C2099 может также возникать, если компилятор не может выполнить свертывание констант в **/fp:strict** , так как параметры среды, задающие точность вычислений с плавающей запятой (дополнительные сведения см. в разделе [_controlfp_s](../../c-runtime-library/reference/controlfp-s.md) ), могут отличаться во время компиляции и во время выполнения.

Когда происходит сбой свертывания констант, компилятор вызывает динамическую инициализацию, которая в С не разрешена.

Чтобы устранить эту ошибку, скомпилируйте модуль как CPP-файл или упростите выражение.

Дополнительные сведения см. в разделе [/fp (определение поведения с плавающей запятой)](../../build/reference/fp-specify-floating-point-behavior.md).

Следующий пример приводит к возникновению ошибки C2099.

```c
// C2099_2.c
// compile with: /fp:strict /c
float X = 2.0 - 1.0;   // C2099
float X2 = 1.0;   // OK
```
