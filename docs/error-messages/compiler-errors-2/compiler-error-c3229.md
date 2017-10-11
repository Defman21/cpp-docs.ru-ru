---
title: "Ошибка компилятора C3229 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3229
dev_langs:
- C++
helpviewer_keywords:
- C3229
ms.assetid: f2d90923-aa8b-444f-ab10-1f37dbb864e1
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 4687643e69ff0c31f4aac9cd30c4fc307c8b02e4
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3229"></a>Ошибка компилятора C3229
"тип": косвенные обращения к параметру универсального типа не допускаются  
  
 Нельзя использовать универсальные параметры с `*`, `^`или `&`.  
  
## <a name="example"></a>Пример  
 В следующем примере возникает ошибка C3229.  
  
```  
// C3229.cpp  
// compile with: /clr /c  
generic <class T>  
ref class C {  
   T^ t;   // C3229  
};  
  
// OK  
generic <class T>  
ref class D {  
   T u;  
};  
```  
  
## <a name="example"></a>Пример  
 В следующем примере возникает ошибка C3229.  
  
```  
// C3229_b.cpp  
// compile with: /clr /c  
generic <class T>   // OK  
ref class Utils {  
   static void sort(T elems[], size_t size);   // C3229  
   static void sort2(T elems, size_t size);   // OK  
};  
```