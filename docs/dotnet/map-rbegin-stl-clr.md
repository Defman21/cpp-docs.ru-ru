---
title: "map::rbegin (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::map::rbegin"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "rbegin - член [STL/CLR]"
ms.assetid: bd7165a3-561f-48d4-9791-7aaafc2cf3a5
caps.latest.revision: 15
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 13
---
# map::rbegin (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Задает начало обратной управляемой последовательности.  
  
## Синтаксис  
  
```  
reverse_iterator rbegin();  
```  
  
## Заметки  
 Функция\-член возвращает обратный итератор, обозначает последний элемент контролируемой последовательности или только за началом пустой последовательности.  Таким образом, он задает для обратной последовательности параметр `beginning`.  Используется для получения итератора, который задает начало управляемой последовательности с параметром `current`, отображаемой в обратном порядке, однако в случае изменения длины управляемой последовательности его состояние может измениться.  
  
## Пример  
  
```  
// cliext_map_rbegin.cpp   
// compile with: /clr   
#include <cliext/map>   
  
typedef cliext::map<wchar_t, int> Mymap;   
int main()   
    {   
    Mymap c1;   
    c1.insert(Mymap::make_value(L'a', 1));   
    c1.insert(Mymap::make_value(L'b', 2));   
    c1.insert(Mymap::make_value(L'c', 3));   
  
// display contents " [a 1] [b 2] [c 3]"   
    for each (Mymap::value_type elem in c1)   
        System::Console::Write(" [{0} {1}]", elem->first, elem->second);   
    System::Console::WriteLine();   
  
// inspect first two items in reversed sequence   
    Mymap::reverse_iterator rit = c1.rbegin();   
    System::Console::WriteLine("*rbegin() = [{0} {1}]",   
        rit->first, rit->second);   
    ++rit;   
    System::Console::WriteLine("*++rbegin() = [{0} {1}]",   
        rit->first, rit->second);   
    return (0);   
    }  
  
```  
  
  **\[1\] \[2\] \[BC — 3\]**  
**\*rbegin\(\) \= \[C — 3\]**  
**\*\+\+rbegin\(\) \= \[B 2\]**   
## Требования  
 **Заголовок:**\<cliext\/map\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [map](../dotnet/map-stl-clr.md)   
 [map::begin](../dotnet/map-begin-stl-clr.md)   
 [map::end](../dotnet/map-end-stl-clr.md)   
 [map::rend](../dotnet/map-rend-stl-clr.md)