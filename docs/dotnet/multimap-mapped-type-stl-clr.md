---
title: "multimap::mapped_type (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::multimap::mapped_type"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "mapped_type - элемент [STL/CLR]"
ms.assetid: 0b59c9a9-7f6a-4c3d-bdc6-0b90c28eff34
caps.latest.revision: 13
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 11
---
# multimap::mapped_type (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Тип сопоставленного значения, связанного с каждым ключом.  
  
## Синтаксис  
  
```  
typedef Mapped mapped_type;  
```  
  
## Заметки  
 Тип синоним для параметра `Mapped` шаблона.  
  
## Пример  
  
```  
// cliext_multimap_mapped_type.cpp   
// compile with: /clr   
#include <cliext/map>   
  
typedef cliext::multimap<wchar_t, int> Mymultimap;   
int main()   
    {   
    Mymultimap c1;   
    c1.insert(Mymultimap::make_value(L'a', 1));   
    c1.insert(Mymultimap::make_value(L'b', 2));   
    c1.insert(Mymultimap::make_value(L'c', 3));   
  
// display contents " [a 1] [b 2] [c 3]" using mapped_type   
    for (Mymultimap::iterator it = c1.begin(); it != c1.end(); ++it)   
        {   // store element in mapped_type object   
        Mymultimap::mapped_type val = it->second;   
  
        System::Console::Write(" {0}", val);   
        }   
    System::Console::WriteLine();   
    return (0);   
    }  
  
```  
  
  **1 2 3**   
## Требования  
 **Заголовок:**\<cliext\/map\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [multimap](../dotnet/multimap-stl-clr.md)   
 [multimap::key\_compare](../dotnet/multimap-key-compare-stl-clr.md)   
 [multimap::value\_type](../dotnet/multimap-value-type-stl-clr.md)