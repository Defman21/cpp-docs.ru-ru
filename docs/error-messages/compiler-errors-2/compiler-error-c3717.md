---
title: "Ошибка компилятора C3717 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3717
dev_langs:
- C++
helpviewer_keywords:
- C3717
ms.assetid: ae4fceb1-2583-4577-b2f1-40971a017055
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: f7256762ef4cf9c3850bd95bb09d23394c2e64f3
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3717"></a>Ошибка компилятора C3717
«метод»: метод, порождающий события не может быть определен  
  
 Был объявлен метод событий, который включает в себя реализацию. [__Event](../../cpp/event.md) объявление метода не может иметь определение. Чтобы устранить эту ошибку, убедитесь, что объявления методов событий не имеют определений. Например, в следующем коде удалить тело функции из `event1` объявления, как указано в комментариях.  
  
 Следующий пример приводит к возникновению ошибки C3717:  
  
```  
// C3717.cpp  
[event_source(native)]  
class CEventSrc {  
public:  
   __event void event1() {   // C3717  
   }  
  
   // remove definition for event1 and substitute following declaration  
   // __event void event1();  
};  
  
[event_receiver(native)]  
class CEventRec {  
public:  
   void handler1() {  
   }  
  
   void HookEvents(CEventSrc* pSrc) {  
      __hook(CEventSrc::event1, pSrc, CEventRec::handler1);  
   }  
  
   void UnhookEvents(CEventSrc* pSrc) {  
      __unhook(CEventSrc::event1, pSrc, CEventRec::handler1);  
   }  
};  
  
int main() {  
}  
```