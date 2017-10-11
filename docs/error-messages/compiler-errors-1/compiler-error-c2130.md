---
title: "Ошибка компилятора C2130 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C2130
dev_langs:
- C++
helpviewer_keywords:
- C2130
ms.assetid: c6fd5a7e-8f28-4f67-99d1-95a13b0dff90
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: b510d68a1434f1c82c7d327391d9c7a34b954724
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2130"></a>Ошибка компилятора C2130
\#строки требуется строка, содержащая имя файла, найден «токен»  
  
 Дополнительный токен имени файла после директивы [#line](../../preprocessor/hash-line-directive-c-cpp.md) `linenumber` должен быть строкой.  
  
 При компиляции следующего примера возникнет ошибка C2130:  
  
```  
// C2130.cpp  
int main() {  
   #line 1000 test   // C2130  
   #line 1000 "test"   // OK  
}  
```