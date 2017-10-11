---
title: "Ошибка компилятора C2443 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2443
dev_langs:
- C++
helpviewer_keywords:
- C2443
ms.assetid: 315330d5-24bc-4193-a531-0642095be58f
caps.latest.revision: 8
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: f0148da7082c4165dbca959857b7766f985fbf0a
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2443"></a>Ошибка компилятора C2443
конфликт размеров операндов  
  
 Инструкции по требуются операнды, чтобы быть одинакового размера.  
  
 Следующий пример приводит к возникновению ошибки C2443:  
  
```  
// C2443.cpp  
// processor: x86  
short var;  
int main() {  
   __asm xchg ax,bl   // C2443  
   __asm mov al,red   // C2443  
   __asm mov al,BYTE PTR var   // OK  
}  
```