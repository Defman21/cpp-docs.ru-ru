---
title: "Ошибка компилятора C2251 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C2251
dev_langs:
- C++
helpviewer_keywords:
- C2251
ms.assetid: fefe050c-f8d3-4316-b237-8007dbcdd3bf
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 72ca85b05a8ac67fab5d152871eaed393e154c11
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2251"></a>Ошибка компилятора C2251
в пространстве имен "пространство_имен" отсутствует член "член" — имелся в виду "член"?  
  
 Компилятору не удалось обнаружить идентификатор в указанном пространстве имен.  
  
 В следующем примере возникает ошибка C2251:  
  
```  
// C2251.cpp  
// compile with: /c  
namespace A {  
   namespace B {  
      void f1();  
   }  
  
   using namespace B;  
}  
  
void A::f1() {}   // C2251  
void A::B::f1() {}   // OK  
```