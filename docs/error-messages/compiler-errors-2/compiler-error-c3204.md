---
title: "Ошибка компилятора C3204 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3204
dev_langs:
- C++
helpviewer_keywords:
- C3204
ms.assetid: 06e578da-0262-48c8-b2ae-be1cd6d28884
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 7d28da9839a82c63017d8cbd24e585e3af8aab2f
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3204"></a>Ошибка компилятора C3204
нельзя вызвать "_alloca" в пределах блока catch  
  
 Эта ошибка возникает при использовании вызова [_alloca](../../c-runtime-library/reference/alloca.md) из блока catch.  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C3204:  
  
```  
// C3204.cpp  
// compile with: /EHsc  
#include <malloc.h>  
  
void ShowError(void)  
{  
   try  
   {  
   }  
   catch(...)  
   {  
      _alloca(1);   // C3204  
   }  
}  
```