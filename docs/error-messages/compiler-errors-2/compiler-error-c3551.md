---
title: "Ошибка компилятора C3551 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3551
dev_langs:
- C++
helpviewer_keywords:
- C3551
ms.assetid: c8ee23da-6568-40db-93a6-3ddb7ac47712
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 450bd97efc9cfbf07eac84a3e6a693af698fc64f
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3551"></a>Ошибка компилятора C3551
Ожидался тип возвращаемого значения с поздним заданием  
  
 Если вы используете ключевое слово `auto` для типа возвращаемого значения функции, необходимо использовать тип возвращаемого значения с поздним заданием. В следующем примере тип возвращаемого значения с поздним заданием для функции `myFunction` является указателем на массив из четырех элементов типа `int`.  
  
```  
auto myFunction()->int(*)[4];   
```  
  
## <a name="see-also"></a>См. также  
 [auto](../../cpp/auto-cpp.md)