---
title: "Ошибка компилятора C3270 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3270
dev_langs:
- C++
helpviewer_keywords:
- C3270
ms.assetid: 70e6e76b-7415-48f5-a61e-2ed50caf08e4
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 326f53f06c6cc4d93eb85f265df161c7b2b86535
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3270"></a>Ошибка компилятора C3270
"поле": атрибут FieldOffset можно использовать только в контексте StructLayout(Explicit), в котором он обязателен  
  
Поле помечено атрибутом **FieldOffset**, который может использоваться только когда **StructLayout(Explicit)** действует.  
  
Следующий пример приводит к возникновению ошибки C3270:  
  
```  
// C3270_2.cpp  
// compile with: /clr /c  
using namespace System::Runtime::InteropServices;  
  
[ StructLayout(LayoutKind::Sequential) ]  
// try the following line instead  
// [ StructLayout(LayoutKind::Explicit) ]  
public value struct MYUNION  
{  
   [FieldOffset(0)] int a;   // C3270  
   // ...  
};  
```  
