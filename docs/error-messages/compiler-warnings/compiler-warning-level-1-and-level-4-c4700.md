---
title: "Предупреждение компилятора (уровень 1 и уровень 4) C4700 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C4700
dev_langs:
- C++
helpviewer_keywords:
- C4700
ms.assetid: 2da0deb4-77dd-4b05-98d3-b78d74ac4ca7
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: f41e519a9dbcff3cc5ad4b718003e5964bfc3e85
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-warning-level-1-and-level-4-c4700"></a>Предупреждение компилятора (уровень 1 и уровень 4) C4700
неинициализированная локальная переменная «имя» используется  
  
 Использовать локальную переменную *имя* без предварительного присвоения значения, что может привести к непредсказуемым результатам.  
  
 Следующий пример приводит к возникновению ошибки C4700:  
  
```  
// C4700.cpp  
// compile with: /W1  
int main() {  
   int i;  
   return i;   // C4700  
}  
```  
  
 В разделе [/CLR: safe](../../build/reference/clr-common-language-runtime-compilation.md) это предупреждение уровня 4.  Следующий пример приводит к возникновению ошибки C4700:  
  
```  
// C4700b.cpp  
// compile with: /W4 /clr:safe /c  
using namespace System;  
int main() {  
   Int32^ bi;  
   return *bi;   // C4700  
}  
```