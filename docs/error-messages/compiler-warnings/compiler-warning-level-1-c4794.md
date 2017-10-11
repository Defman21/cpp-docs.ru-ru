---
title: "Ошибка компилятора предупреждение (уровень 1) C4794 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C4794
dev_langs:
- C++
helpviewer_keywords:
- C4794
ms.assetid: badc9c36-fa1a-4fec-929b-7bfda7a7b79f
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: ghogen
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0d9cbb01d1ad0f2ea65d59334cb88140ef18fce0
ms.openlocfilehash: 8f73e3da504960f737f175fff4c9d7b07084833a
ms.contentlocale: ru-ru
ms.lasthandoff: 04/12/2017

---
# <a name="compiler-warning-level-1-c4794"></a>Предупреждение компилятора (уровень 1) C4794
сегмент переменной из локальной памяти потока "переменная" изменен с "имя_раздела" на ".tls$"  
  
 Вы использовали [#pragma data_seg](../../preprocessor/data-seg.md) поместить переменную tls в раздел, не начинающийся с .tls$.  
  
 Раздел .tls$*x* раздел будет существовать в объектном файле где [__declspec(thread)](../../cpp/thread.md) определены переменные. Раздел .tls в файле EXE или DLL будет получен из этих разделов.  
  
## <a name="example"></a>Пример  
 В следующем примере возникает ошибка C4794.  
  
```  
// C4794.cpp  
// compile with: /W1 /c  
#pragma data_seg(".someseg")  
__declspec(thread) int i;   // C4794  
  
// OK  
#pragma data_seg(".tls$9")  
__declspec(thread) int j;  
```