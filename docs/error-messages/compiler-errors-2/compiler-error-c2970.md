---
title: "Ошибка компилятора C2970 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2970
dev_langs:
- C++
helpviewer_keywords:
- C2970
ms.assetid: 21d90348-20d3-438c-b278-efdbfb93a7d2
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: fc125b400a718805af2ee0829100c056fffa29a3
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2970"></a>Ошибка компилятора C2970
«класс»: параметр шаблона «параметр»: «аргумент»: выражение, включающее объекты с внутренней компоновкой не может использоваться как аргумент не является типом  
  
 Нельзя использовать имя или адрес статической переменной в качестве аргумента шаблона. Класс шаблона ожидает константу, которая может быть вычислено во время компиляции.  
  
 Следующий пример приводит к возникновению ошибки C2970:  
  
```  
// C2970.cpp  
// compile with: /c  
static int si;  
// could declare nonstatic to resolve all errors  
// int si;  
  
template <int i>   
class X {};  
  
template <int *pi>   
class Y {};  
  
X<si> anX;   // C2970 cannot use static variable in templates  
  
// this would also work  
const int i = 10;  
X<i> anX2;  
```