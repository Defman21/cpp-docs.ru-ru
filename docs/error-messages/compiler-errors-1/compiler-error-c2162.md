---
title: "Ошибка компилятора C2162 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2162
dev_langs:
- C++
helpviewer_keywords:
- C2162
ms.assetid: 34923628-d35e-48ab-9072-b95e3b5f6b45
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 63c27d28a5c1546c65fe3df069482f9495d4f851
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2162"></a>Ошибка компилятора C2162
требуется формальный параметр макроса  
  
 Токен после строковый оператор (#) не является именем формальных параметров.  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C2162:  
  
```  
// C2162.cpp  
// compile with: /c  
#include <stdio.h>  
  
#define print(a) printf_s(b)   // OK  
#define print(a) printf_s(#b)    // C2162  
```