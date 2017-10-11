---
title: "Ошибка компилятора C3765 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3765
dev_langs:
- C++
helpviewer_keywords:
- C3765
ms.assetid: feadee7a-fcfb-402c-af2f-0e656f814a13
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 44311ab210a85b05d86eb48aebe8294c95bfb5ab
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3765"></a>Ошибка компилятора C3765
«событие»: не удается определить событие в классе или структуре «тип» с пометкой event_receiver  
  
 Если класс, помеченный с [event_receiver](../../windows/event-receiver.md) атрибут, он не может содержать [__event](../../cpp/event.md) объявления.  
  
 В следующем примере возникает ошибка C3765:  
  
```  
// C3765.cpp  
[event_receiver(native)]  
struct ER2 {  
   __event void f();   // C3765  
   __event void b(int);   // C3765  
};  
```