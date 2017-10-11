---
title: "Ошибка компилятора C3118 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3118
dev_langs:
- C++
helpviewer_keywords:
- C3118
ms.assetid: 40fbe681-8868-4cb2-a2b2-4db4449319a7
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 51cc783d29e8a3b63a8c9ecf50b1ea280dae9a9a
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3118"></a>Ошибка компилятора C3118
«интерфейс»: интерфейсы не поддерживают виртуальное наследование  
  
 Предпринята попытка виртуального наследования от интерфейса. Например:  
  
```  
// C3118.cpp  
__interface I1 {  
};  
  
__interface I2 : virtual I1 {   // C3118  
};  
```  
  
 создает эту ошибку.