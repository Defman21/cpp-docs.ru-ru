---
title: "set::generic_iterator (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::set::generic_iterator"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "generic_iterator - элемент [STL/CLR]"
ms.assetid: 2ecc9fde-9fad-49a5-821e-e79304be6c3b
caps.latest.revision: 13
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 11
---
# set::generic_iterator (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Тип итератора для использования с универсальным интерфейсом для контейнера.  
  
## Синтаксис  
  
```  
typedef Microsoft::VisualC::StlClr::Generic::  
    ContainerBidirectionalIterator<generic_value>  
    generic_iterator;  
```  
  
## Заметки  
 Описывает итератор универсальный тип, который можно использовать с универсальным интерфейсом для этого класса контейнера шаблона.  
  
## Пример  
  
```  
// cliext_set_generic_iterator.cpp   
// compile with: /clr   
#include <cliext/set>   
  
typedef cliext::set<wchar_t> Myset;   
int main()   
    {   
    Myset c1;   
    c1.insert(L'a');   
    c1.insert(L'b');   
    c1.insert(L'c');   
  
// display contents " a b c"   
    for each (wchar_t elem in c1)   
        System::Console::Write(" {0}", elem);   
    System::Console::WriteLine();   
  
// construct a generic container   
    Myset::generic_container^ gc1 = %c1;   
    for each (wchar_t elem in gc1)   
        System::Console::Write(" {0}", elem);   
    System::Console::WriteLine();   
  
// get an element and display it   
    Myset::generic_iterator gcit = gc1->begin();   
    Myset::generic_value gcval = *gcit;   
    System::Console::WriteLine(" {0}", gcval);   
    return (0);   
    }  
  
```  
  
  **a b c**  
 **a b c**  
 **a**   
## Требования  
 **Заголовок:**\<cliext\/set\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [набор](../dotnet/set-stl-clr.md)   
 [set::generic\_container](../dotnet/set-generic-container-stl-clr.md)