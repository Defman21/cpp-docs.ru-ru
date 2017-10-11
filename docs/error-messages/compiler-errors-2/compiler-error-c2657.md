---
title: "Ошибка компилятора C2657 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2657
dev_langs:
- C++
helpviewer_keywords:
- C2657
ms.assetid: f7cf29a9-684a-4605-9469-ecfee9ba4b03
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 2e0e06104458961297a4d0a3de8b7cda756d16ab
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2657"></a>Ошибка компилятора C2657
"класс:: *" в начале оператора (забыли указать тип?)  
  
 Строка начинается с идентификатора указателя на член.  
  
 Эта ошибка может быть вызвана отсутствует спецификатор типа в объявлении указателя на член.  
  
 Следующий пример приводит к возникновению ошибки C2657:  
  
```  
// C2657.cpp  
class C {};  
int main() {  
   C::* pmc1;        // C2657  
   int C::* pmc2;   // OK  
}  
```