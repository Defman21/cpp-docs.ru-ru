---
description: 'Дополнительные сведения о: Ошибка компилятора C3850'
title: Ошибка компилятора C3850
ms.date: 09/05/2018
f1_keywords:
- C3850
helpviewer_keywords:
- C3850
ms.assetid: 028f3a37-f3ad-4ebc-9168-3cdea47524d4
ms.openlocfilehash: 9563ee8b4ebb2f8c08b67ff88401ef2e3022a03a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97255344"
---
# <a name="compiler-error-c3850"></a>Ошибка компилятора C3850

> "*char*": универсальное имя символа указывает недопустимый символ

## <a name="remarks"></a>Комментарии

Символы, представленные универсальными именами символов, должны представлять допустимые кодовые точки Юникода в диапазоне 0–10FFFF. Универсальное имя символа не может содержать значение в суррогатном диапазоне Юникода (D800–DFFF) или закодированной суррогатной паре. Компилятор создает суррогатную пару из допустимой кодовой точки автоматически.

В коде, скомпилированном как C, универсальное имя символа не может представлять символ в диапазоне 0000-009F включительно, за исключением 0024 (' $ '), 0040 (' \@ ') и 0060 (' ' ').

В коде, скомпилированном как C++, универсальное имя символа может использовать любую допустимую кодовую точку Юникода в строковом или символьном литерале. За пределами литерала универсальное имя символа не должно представлять управляющий символ в диапазонах 0000–001F или 007F–009F (включительно для обоих диапазонов) или элемент основной кодировки исходного кода.  Дополнительные сведения см. в разделе [Character Sets](../../cpp/character-sets.md).

## <a name="example"></a>Пример

В следующем примере показано возникновение ошибки C3850 и приводятся сведения по ее устранению.

```cpp
// C3850.cpp
int main() {
   int \u0019 = 0;   // C3850, not in allowed range for an identifier
   const wchar_t * wstr_bad  = L"\UD840DC8A"; // C3850, UCN is surrogate pair
   const wchar_t * wstr_good = L"\U0002008A"; // Okay, UCN is valid code point
}
```
