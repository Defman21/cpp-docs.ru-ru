---
title: "Предупреждение (уровень 1) C4028 компилятора | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C4028
dev_langs:
- C++
helpviewer_keywords:
- C4028
ms.assetid: c3e8b70b-e870-416c-a285-bba5f71dbfc6
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 0041d795ed5afce50592f21f41986d3f32c71fe3
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-warning-level-1-c4028"></a>Предупреждение (уровень 1) C4028 компилятора
формальный параметр «число» отличается от объявления  
  
 Тип формального параметра, не совпадает с соответствующим параметром в объявлении. Используется тип из оригинального объявления.  
  
 Это предупреждение действует только для исходного кода C.  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C4028.  
  
```  
// C4028.c  
// compile with: /W1 /Za  
void f(int , ...);  
void f(int i, int j) {}   // C4028  
  
void g(int , int);  
void g(int i, int j) {}   // OK  
  
int main() {}  
```