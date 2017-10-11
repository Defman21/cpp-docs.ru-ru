---
title: "Ошибка компилятора C2391 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2391
dev_langs:
- C++
helpviewer_keywords:
- C2391
ms.assetid: 63a9c6b9-03cc-4517-885c-bdcd048643b3
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 573cea44b0a39ff3cc0dff4469aa8c5f5a2459e5
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2391"></a>Ошибка компилятора C2391
«Идентификатор»: «friend» нельзя использовать во время определения типа  
  
 `friend` Объявление включает объявление полного класса. Объект `friend` объявления можно указать функцию-член или сложный спецификатор типа, но не объявление полного класса.  
  
 При компиляции следующего примера возникнет ошибка C2326:  
  
```  
// C2391.cpp  
// compile with: /c  
class D {   
   void func( int );   
};  
  
class A {  
   friend class B { int i; };   // C2391  
  
   // OK  
   friend class C;  
   friend void D::func(int);  
};  
```