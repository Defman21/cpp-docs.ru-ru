---
title: "Ошибка компилятора C3739 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3739
dev_langs:
- C++
helpviewer_keywords:
- C3739
ms.assetid: acffe894-08b8-4bf2-9249-9501e6e2bad3
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: b3fa62f908f152e127669d1cd935fafdb75d413f
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3739"></a>Ошибка компилятора C3739
«класс»: синтаксис поддерживается только в том случае, если параметр «layout_dependent» для event_receiver имеет значение true  
  
 Предпринята попытка подключить весь интерфейс событий, но `layout_dependent` на [event_receiver](../../windows/event-receiver.md) атрибута не является значение true, необходимо подключать одиночного события за раз.  
  
 Следующий пример приводит к возникновению ошибки C3739:  
  
```  
// C3739.cpp  
struct A  
{  
   __event void e();  
};  
  
// event_receiver is implied  
// [ event_receiver(layout_dependent=false)]  
  
// use the following line instead  
// [event_receiver(com, layout_dependent=true), coclass ]  
struct B  
{  
   void f();  
   B(A* a)  
   {  
      __hook(A, a, &B::f);   // C3739  
      // use the following line instead to hook a single event  
      // __hook(&A::e, a, &B::f);  
   }  
};  
  
int main()  
{  
}  
```