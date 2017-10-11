---
title: "Ошибка компилятора C2201 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2201
dev_langs:
- C++
helpviewer_keywords:
- C2201
ms.assetid: ed927659-6e9c-447d-9963-19969ae1e957
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: e68912ce5468f07bf18fb953adc996b755500aca
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2201"></a>Ошибка компилятора C2201
«Идентификатор»: для экспорта или импорта требуется внешняя компоновка  
  
 Тип экспортируемого идентификатора — `static`.  
  
 При компиляции следующего примера возникнет ошибка C2286:  
  
```  
// C2201.cpp  
// compile with: /c  
__declspec(dllexport) static void func() {}   // C2201 func() is static  
__declspec(dllexport) void func2() {}   // OK  
```  
  
## <a name="see-also"></a>См. также  
 [Типы компоновки](../../cpp/types-of-linkage.md)