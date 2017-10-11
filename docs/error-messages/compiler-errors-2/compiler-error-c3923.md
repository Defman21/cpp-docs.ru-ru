---
title: "Ошибка компилятора C3923 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3923
dev_langs:
- C++
helpviewer_keywords:
- C3923
ms.assetid: db8838e9-6344-4cd6-83e0-a8abeb12c4c0
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 863273ec0e9922a6a0b4e7355fe47178a7dd5bbe
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3923"></a>Ошибка компилятора C3923
member: в функции-члене класса WinRT или управляемого класса невозможно использовать определения локальных классов, структур или объединений  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C3923:  
  
```  
// C3923.cpp  
// compile with: /clr /c  
ref struct x {  
   void Test() {  
      struct a {};   // C3923  
      class b {};   // C3923  
      union c {};   // C3923  
   }  
};  
```