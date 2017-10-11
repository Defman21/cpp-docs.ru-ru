---
title: "Ошибка компилятора C2232 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C2232
dev_langs:
- C++
helpviewer_keywords:
- C2232
ms.assetid: 76f302b7-30a7-4a81-9a39-b4edde33b54c
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 0c02f9b3953abf107cf4e3c33316c9d68f00b7b4
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2232"></a>Ошибка компилятора C2232
«->»: левый операнд имеет ключ класса «тип «, используйте».»  
  
 Операнд в левой части оператора `->` не является указателем. Используйте оператор точки (.) для класса, структуры или объединения.  
  
 При компиляции следующего примера возникнет ошибка C2232:  
  
```  
// C2232.c  
struct X {  
    int member;  
} x, *px;  
int main() {  
    x->member = 0;   // C2232, x is not a pointer  
  
    px->member = 0;  
    x.member = 0;  
}  
```