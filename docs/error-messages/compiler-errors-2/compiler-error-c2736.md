---
description: 'Дополнительные сведения о: Ошибка компилятора C2736'
title: Ошибка компилятора C2736
ms.date: 11/04/2016
f1_keywords:
- C2736
helpviewer_keywords:
- C2736
ms.assetid: 95a6bc28-c0cb-49dc-87e6-e993dbbba881
ms.openlocfilehash: 635f20d684fb929277f29299f0f074cc3a19e9df
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97123166"
---
# <a name="compiler-error-c2736"></a>Ошибка компилятора C2736

ключевое слово "keyword" не разрешено в приведении

Ключевое слово недопустимо в приведении.

Следующий пример приводит к возникновению ошибки C2736:

```cpp
// C2736.cpp
int main() {
   return (virtual) 0;   // C2736
   // try the following line instead
   // return 0;
}
```
