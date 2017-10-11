---
title: "Ошибка компилятора C2393 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2393
dev_langs:
- C++
helpviewer_keywords:
- C2393
ms.assetid: 4bd95728-e813-4ce8-844a-c6ebe235ca82
caps.latest.revision: 11
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: a2c4f8d31fb6ddb6eaa9472dc7537edbcdc29054
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2393"></a>Ошибка компилятора C2393
«символ»: символ appdomain не может быть помещен в сегмент «сегмент»  
  
 Параметры компилятора **/CLR: pure** и **/CLR: safe** в Visual Studio 2015 не рекомендуется использовать.  
  
 Использование [appdomain](../../cpp/appdomain.md) переменных подразумевает, что компиляция выполняется с **/CLR: pure** или **/CLR: safe**, и безопасный или чистый образ не может содержать сегменты данных.  
  
 В разделе [/CLR (компиляция CLR)](../../build/reference/clr-common-language-runtime-compilation.md) для получения дополнительной информации.  
  
## <a name="example"></a>Пример  
 Следующий пример приводит к возникновению ошибки C2393.  
  
```  
// C2393.cpp  
// compile with: /clr:pure /c  
#pragma data_seg("myseg")  
int n = 0;   // C2393  
```