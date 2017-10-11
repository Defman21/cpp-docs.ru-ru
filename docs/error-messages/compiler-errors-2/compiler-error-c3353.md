---
title: "Ошибка компилятора C3353 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3353
dev_langs:
- C++
helpviewer_keywords:
- C3353
ms.assetid: 5699c04b-d504-46ce-bf71-c200318fed71
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 47a0231a161a2502c26786fceeb1b3634b236eaf
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3353"></a>Ошибка компилятора C3353
delegate: создание делегата допускается только из глобальной функции или функции-члена управляемого типа или типа WinRT  
  
 Делегаты, объявленные с [делегировать](../../windows/delegate-cpp-component-extensions.md) ключевое слово, можно объявлять только в глобальной области видимости.  
  
 Следующий пример приводит к возникновению ошибки C3353:  
  
```  
// C3353.cpp  
// compile with: /clr  
delegate int f;   // C3353  
```