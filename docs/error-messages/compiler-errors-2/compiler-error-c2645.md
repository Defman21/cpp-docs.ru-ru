---
title: "Ошибка компилятора C2645 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2645
dev_langs:
- C++
helpviewer_keywords:
- C2645
ms.assetid: 6609c2fa-c3b2-4a6b-8e8d-58fb52f67175
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: aaccf62efbc5926f65ac2e59359e0c73e8d0e680
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2645"></a>Ошибка компилятора C2645
отсутствует полное имя для указателя на член (найдено ":: *")  
  
 Объявление указателя на член не задает класс.  
  
 Следующий пример приводит к возникновению ошибки C2645:  
  
```  
// C2645.cpp  
class A {};  
int main() {  
   int B::* bp;   // C2645 B not defined  
   int A::* ap;   // OK  
}  
```