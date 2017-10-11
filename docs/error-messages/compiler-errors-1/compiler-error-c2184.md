---
title: "Ошибка компилятора C2184 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C2184
dev_langs:
- C++
helpviewer_keywords:
- C2184
ms.assetid: 80fc8bff-7d76-4bde-94d2-01d84bb6824a
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 7e5402835be51b67bece4853996f281cf0ab5cfb
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2184"></a>Ошибка компилятора C2184
"тип": недопустимый тип для выражения __except, должен быть целым  
  
 В выражении [__except](../../c-language/try-except-statement-c.md) используется недопустимый тип.  
  
 Следующий пример приводит к возникновению ошибки C2184:  
  
```  
// C2184.cpp  
void f() {  
   int * p;  
   __try{}  
   __except(p){};   // C2184  
}  
```  
  
 Возможное решение:  
  
```  
// C2184b.cpp  
// compile with: /c  
void f() {  
   int i = 0;  
   __try{}  
   __except(i){};  
}  
```