---
title: "Ошибка компилятора C3640 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3640
dev_langs:
- C++
helpviewer_keywords:
- C3640
ms.assetid: fcc56894-0f98-48af-8561-3bf7c7b2b93f
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 493206e55be18d1e7cc00fec55dd2e111ad5026f
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3640"></a>Ошибка компилятора C3640
«член»: член адресуемая или виртуальная функция локального класса должна быть определена  
  
 Для компилятора требуются некоторые функции определен.  
  
 В следующем примере возникает ошибка C3640:  
  
```  
// C3640.cpp  
void f()   
{  
   struct S  
   {  
      virtual void f1();   // C3640  
      // Try the following line instead:  
      // virtual void f1(){}  
   };  
}  
```