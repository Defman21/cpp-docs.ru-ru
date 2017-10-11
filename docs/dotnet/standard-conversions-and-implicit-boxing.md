---
title: "Стандартные преобразования и неявная упаковка-преобразование | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "упаковка-преобразование, неявные"
ms.assetid: 33f7fc7d-5674-44a2-a859-0e6a04fae519
caps.latest.revision: 6
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 4
---
# Стандартные преобразования и неявная упаковка-преобразование
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Стандартное преобразование будет выбрано компилятором с преобразованием, для упаковка\-преобразования.  
  
## Пример  
  
```  
// clr_implicit_boxing_Std_conversion.cpp  
// compile with: /clr  
int f3(int ^ i) {   // requires boxing  
   return 1;  
}  
  
int f3(char c) {   // no boxing required, standard conversion  
   return 2;  
}  
  
int main() {  
   int i = 5;  
   System::Console::WriteLine(f3(i));  
}  
```  
  
 **2**   
## См. также  
 [Упаковка\-преобразование](../windows/boxing-cpp-component-extensions.md)