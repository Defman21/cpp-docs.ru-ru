---
title: "hash_map::value_type (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::hash_map::value_type"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "value_type - элемент [STL/CLR]"
ms.assetid: 7aa29304-5e52-46be-b50e-45e11401764e
caps.latest.revision: 14
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 12
---
# hash_map::value_type (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Тип элемента.  
  
## Синтаксис  
  
```  
typedef generic_value value_type;  
```  
  
## Заметки  
 Тип является синонимом `generic_value`.  
  
## Пример  
  
```  
// cliext_hash_map_value_type.cpp   
// compile with: /clr   
#include <cliext/hash_map>   
  
typedef cliext::hash_map<wchar_t, int> Myhash_map;   
int main()   
    {   
    Myhash_map c1;   
    c1.insert(Myhash_map::make_value(L'a', 1));   
    c1.insert(Myhash_map::make_value(L'b', 2));   
    c1.insert(Myhash_map::make_value(L'c', 3));   
  
// display contents " [a 1] [b 2] [c 3]" using value_type   
    for (Myhash_map::iterator it = c1.begin(); it != c1.end(); ++it)   
        {   // store element in value_type object   
        Myhash_map::value_type val = *it;   
        System::Console::Write(" [{0} {1}]", val->first, val->second);   
        }   
    System::Console::WriteLine();   
    return (0);   
    }  
  
```  
  
  **\[1\] \[2\] \[BC — 3\]**   
## Требования  
 **Заголовок:**\<cliext\/hash\_map\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [hash\_map](../dotnet/hash-map-stl-clr.md)   
 [hash\_map::const\_reference](../dotnet/hash-map-const-reference-stl-clr.md)   
 [hash\_map::key\_type](../Topic/hash_map::key_type%20\(STL-CLR\).md)   
 [hash\_map::reference](../dotnet/hash-map-reference-stl-clr.md)