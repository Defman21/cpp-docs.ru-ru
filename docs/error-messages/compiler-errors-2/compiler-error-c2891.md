---
description: 'Дополнительные сведения о: Ошибка компилятора C2891'
title: Ошибка компилятора C2891
ms.date: 11/04/2016
f1_keywords:
- C2891
helpviewer_keywords:
- C2891
ms.assetid: e12cfb2d-df45-4b0d-b155-c51d17e812fa
ms.openlocfilehash: e546340d0ba035da50dd36b18b870b565b6e1bc9
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97337439"
---
# <a name="compiler-error-c2891"></a>Ошибка компилятора C2891

"параметр": невозможно получить адрес параметра шаблона

Нельзя получить адрес параметра шаблона, если он не является левосторонним значением. Параметры типа не значения lvalue, так как они не имеют адреса. Значения, не являющиеся типами, в списках параметров шаблона, не значения lvalue также, не имеют адреса. Это пример кода, который вызывает ошибку компилятора C2891, так как значение, передаваемое в качестве параметра шаблона, является копией аргумента шаблона, создаваемой компилятором.

```
template <int i> int* f() { return &i; }
```

Для параметров шаблона, значения lvalue, таких как ссылочные типы, может быть получен свой адрес.

```
template <int& r> int* f() { return &r; }
```

Чтобы исправить эту ошибку, не задавайте адрес параметра шаблона, если он не является левосторонним значением.
