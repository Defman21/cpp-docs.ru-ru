---
title: "Ошибка компилятора C2276 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2276
dev_langs:
- C++
helpviewer_keywords:
- C2276
ms.assetid: 62005ad9-6cb9-4b1f-965d-b875adaf695e
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 365ffc998d201efb7397f1b08cbbc86032fd2781
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2276"></a>Ошибка компилятора C2276
«оператор»: Недопустимая операция с функция выражение связанного элемента  
  
 Компилятор обнаружил проблему с помощью синтаксиса для создания указателя на член.  
  
 Следующий пример приводит к возникновению ошибки C2276:  
  
```  
// C2276.cpp  
class A {  
public:  
   int func(){return 0;}  
} a;  
  
int (*pf)() = &a.func;   // C2276  
// try the following line instead  
// int (A::*pf3)() = &A::func;  
  
class B {  
public:  
   void mf() {  
      &this -> mf;   // C2276  
      // try the following line instead  
      // &B::mf;  
   }  
};  
  
int main() {  
   A a;  
   &a.func;   // C2276  
   // try the following line instead  
   // &A::func;  
}  
```