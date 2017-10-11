---
title: "Ошибка компилятора C3733 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3733
dev_langs:
- C++
helpviewer_keywords:
- C3733
ms.assetid: 0cc1a9fe-1400-4be3-b35a-16435cba7a5a
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: dedd36afd3b0211148c61ee3279d77eb25273c50
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3733"></a>Ошибка компилятора C3733
«событие»: неверный синтаксис для указания события модели COM; Возможно, отсутствует «__interface»?  
  
 Для события модели COM использован неверный синтаксис. Чтобы устранить эту ошибку, измените тип события или исправьте синтаксис, чтобы соответствовать требованиям, предъявляемым событий COM.  
  
 Следующий пример приводит к возникновению ошибки C3733:  
  
```  
#define _ATL_ATTRIBUTES 1  
#include "atlbase.h"  
#include "atlcom.h"  
  
[coclass, event_source(com), // change 'com' to 'native' to resolve  
uuid("00000000-0000-0000-0000-000000000001")]  
class A  
{  
   __event void func();   // C3733  
};  
  
int main()  
{  
}  
```