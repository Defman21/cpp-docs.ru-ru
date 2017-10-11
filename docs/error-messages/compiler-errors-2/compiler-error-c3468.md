---
title: "Ошибка компилятора C3468 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3468
dev_langs:
- C++
helpviewer_keywords:
- C3468
ms.assetid: cfd320db-2f6e-4e0d-ba02-e79ece87e1e0
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 41fde9cae4697c38dba410fb1fbdb46cd901ae97
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3468"></a>Ошибка компилятора C3468
"тип": тип можно передать только в сборку:  
  
 "`file`" не является сборкой  
  
 Перенаправлять типы можно только в сборке.  
  
 Дополнительные сведения см. в разделе [переадресации типов (C + +/ CLI)](../../windows/type-forwarding-cpp-cli.md).  
  
## <a name="example"></a>Пример  
 В приведенном ниже примере создается модуль.  
  
```  
// C3468.cpp  
// compile with: /LN /clr  
public ref class R {};  
```  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C3468:  
  
```  
// C3468_b.cpp  
// compile with: /clr /c  
#using "C3468.netmodule"  
[ assembly:TypeForwardedTo(R::typeid) ];   // C3468  
```