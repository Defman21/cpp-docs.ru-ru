---
title: "Ошибка компилятора C3368 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3368
dev_langs:
- C++
helpviewer_keywords:
- C3368
ms.assetid: 5bfd5be4-dfa9-4b33-9612-010561b40955
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 86996ade6501ba83e1895f6ba9b30d62526ff442
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3368"></a>Ошибка компилятора C3368
"объявление_функции": недопустимое соглашение о вызове для IDL  
  
 В IDL-файле можно использовать только соглашения о вызовах [__stdcall](../../cpp/stdcall.md) или [__cdecl](../../cpp/cdecl.md) .  
  
 Следующий пример приводит к возникновению ошибки C3368:  
  
```  
// C3368.cpp  
// processor: x86  
[idl_module(name="Name", dllname="Some.dll")];  
  
[idl_module(name="Name")]  
int __fastcall f1();   // C3368  
```