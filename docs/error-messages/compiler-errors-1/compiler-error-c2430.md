---
description: 'Дополнительные сведения о: Ошибка компилятора C2430'
title: Ошибка компилятора C2430
ms.date: 11/04/2016
f1_keywords:
- C2430
helpviewer_keywords:
- C2430
ms.assetid: 07c20f76-63e1-4d22-b2a9-98b0d45c5cac
ms.openlocfilehash: 9f953ee78b6e4b82ce0ebd4a6621f0f06abadadb
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97190059"
---
# <a name="compiler-error-c2430"></a>Ошибка компилятора C2430

более одного регистра индекса в "идентификаторе"

Масштабируется более одного регистра. Компилятор поддерживает масштабированное индексирование, но можно масштабировать только один регистр.

## <a name="example"></a>Пример

Следующий пример приводит к возникновению ошибки C2430.

```cpp
// C2430.cpp
// processor: x86
int main() {
   _asm mov eax, [ebx*2+ecx*4] // C2430
}
```
