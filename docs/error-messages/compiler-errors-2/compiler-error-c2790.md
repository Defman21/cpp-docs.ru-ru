---
title: "Ошибка компилятора C2790 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2790
dev_langs:
- C++
helpviewer_keywords:
- C2790
ms.assetid: 38d4fce1-ba00-413d-8bc1-e8aa43d7bc1f
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 11ea7285d20808f16f2588d50caebe99429c8da0
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2790"></a>Ошибка компилятора C2790
«super»: это ключевое слово может использоваться только в теле функции-члена класса  
  
 Это сообщение об ошибке возникает, если пользователь пытается использовать ключевое слово [super](../../cpp/super.md) вне контекста функции-члена.  
  
 Следующий пример приводит к возникновению ошибки C2790:  
  
```  
// C2790.cpp  
void f() {  
   __super::g();   // C2790  
}  
```