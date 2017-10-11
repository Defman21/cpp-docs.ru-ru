---
title: "Ошибка компилятора C2372 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2372
dev_langs:
- C++
helpviewer_keywords:
- C2372
ms.assetid: 406bea63-c8d3-4231-9d26-c70af6980840
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 334abb814d9a3bbadfb7c0c9060a333c9de880db
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2372"></a>Ошибка компилятора C2372
«Идентификатор»: переопределение; различные типы косвенного обращения  
  
 Идентификатор уже объявлен с другим производным типом.  
  
 При компиляции следующего примера возникнет ошибка C2326:  
  
```  
// C2372.cpp  
// compile with: /c  
extern int *fp;  
extern int fp[];   // C2372  
extern int fp2[];   // OK  
```