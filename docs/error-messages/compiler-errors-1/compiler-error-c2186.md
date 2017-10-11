---
title: "Ошибка компилятора C2186 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C2186
dev_langs:
- C++
helpviewer_keywords:
- C2186
ms.assetid: 284bfb7e-ab85-4fcb-9864-1ddf7f6c94ae
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 1a3b3333fa9450ba5c734f9192b683c0789cecd6
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2186"></a>Ошибка компилятора C2186
"оператор": недопустимый операнд типа void  
  
 Оператор имеет операнд `void` .  
  
 В следующем примере возникает ошибка C2186:  
  
```  
// C2186.cpp  
// compile with: /c  
void func1( void );  
int  func2( void );  
int i = 2 + func1();   // C2186 func1() is type void  
int j = 2 + func2();   // OK both operands are type int  
```