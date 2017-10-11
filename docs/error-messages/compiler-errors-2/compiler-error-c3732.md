---
title: "Ошибка компилятора C3732 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3732
dev_langs:
- C++
helpviewer_keywords:
- C3732
ms.assetid: 2d55a7e1-9c39-4379-a093-2f7beb27e2ca
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: c545391883d4e2becd21fbb4b3279e3f0c1d60f1
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3732"></a>Ошибка компилятора C3732
«интерфейс»: настраиваемый интерфейс, порождающий COM-события не может наследовать от IDispatch  
  
 Интерфейс, поддерживающий события COM не может наследовать от `IDispatch`. Дополнительные сведения см. в разделе [обработка событий в COM](../../cpp/event-handling-in-com.md).  
  
 Следующая ошибка приводит к возникновению ошибки C3732:  
  
```  
// C3732.cpp  
#define _ATL_ATTRIBUTES 1  
#include "atlbase.h"  
#include "atlcom.h"  
  
[module(name="test")];  
  
// to resolve this C3732, use dual instead of object  
// or inherit from IUnknown  
[ object ]  
__interface I : IDispatch  
{  
};  
  
[ event_source(com), coclass ]  
struct A  
{  
   __event __interface I;   // C3732  
};  
  
int main()  
{  
}  
```