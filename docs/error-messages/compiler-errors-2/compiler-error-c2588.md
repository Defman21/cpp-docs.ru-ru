---
title: "Ошибка компилятора C2588 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2588
dev_langs:
- C++
helpviewer_keywords:
- C2588
ms.assetid: 19a0cabd-ca13-44a5-9be3-ee676abf9bc4
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: c6d71e5bfe442f2b3f2225cd4dc6cb88fc73d24a
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c2588"></a>Ошибка компилятора C2588
":: ~ идентификатор": недопустимый глобальный деструктор  
  
 Деструктор определяется что-то отличное от класса, структуры или объединения. Это не допускается.  
  
 Эта ошибка может быть вызвана отсутствует класса, структуры или объединения имени слева от разрешение области (`::`) оператор.  
  
 Следующий пример приводит к возникновению ошибки C2588:  
  
```  
// C2588.cpp  
~F();   // C2588  
```