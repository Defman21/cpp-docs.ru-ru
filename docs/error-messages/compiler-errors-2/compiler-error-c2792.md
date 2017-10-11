---
title: "Ошибка компилятора C2792 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2792
dev_langs:
- C++
helpviewer_keywords:
- C2792
ms.assetid: 392cf748-4f5e-4e62-a364-3118d5658408
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 16a07fcc43ffde40a4ac540d3e5dbaa8891ea48e
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2792"></a>Ошибка компилятора C2792
«super»: это ключевое слово следует указать "::"  
  
 Токен только может следовать ключевое слово `__super` — `::`.  
  
 Следующий пример приводит к возникновению ошибки C2792:  
  
```  
// C2792.cpp  
struct B {  
   void mf();  
};  
  
struct D : B {  
   void mf() {  
      __super.();   // C2792  
  
      // try the following line instead  
      // __super::mf();  
   }  
};  
```