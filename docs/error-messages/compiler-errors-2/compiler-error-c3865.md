---
title: "Ошибка компилятора C3865 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3865
dev_langs:
- C++
helpviewer_keywords:
- C3865
ms.assetid: 9bc62bb0-4fb8-4856-a5cf-c7cb4029a596
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: af0873d70fcb4f947e838afba130279edf705ced
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3865"></a>Ошибка компилятора C3865
«соглашение_о_вызовах»: может использоваться только в собственных функциях-членах  
  
 Соглашение о вызовах использовался на функцию, которая была глобальной функции или функции-члена управляемого. Соглашение о вызовах может использоваться только в функции-члене native (неуправляемой).  
  
 Дополнительные сведения см. в разделе [соглашения о вызовах](../../cpp/calling-conventions.md).  
  
 Следующий пример приводит к возникновению ошибки C3865:  
  
```  
// C3865.cpp  
// compile with: /clr  
// processor: x86  
void __thiscall Func(){}   // C3865  
  
// OK  
struct MyType {  
   void __thiscall Func(){}  
};  
```