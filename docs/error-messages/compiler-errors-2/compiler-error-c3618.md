---
title: "Ошибка компилятора C3618 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3618
dev_langs:
- C++
helpviewer_keywords:
- C3618
ms.assetid: cacc105d-4389-4cb8-ae6c-41a3622e9a86
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 3b014cb60c2e9a65888fa425f4046c118cfc31d2
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3618"></a>Ошибка компилятора C3618
«функция»: метод, помеченный как DllImport не может быть определен  
  
 Метод, помеченный атрибутом <xref:System.Runtime.InteropServices.DllImportAttribute> определен в указанном массиве. БИБЛИОТЕКИ DLL.  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C3618.  
  
```  
// C3618.cpp  
// compile with: /clr /c  
using namespace System;  
using namespace System::Runtime::InteropServices;  
  
[ DllImport("user32.dll", EntryPoint="MessageBox", CharSet=CharSet::Ansi) ]  // CHANGED   
void Func();   
  
void Func() {}   // C3618, remove this function definition to resolve  
```