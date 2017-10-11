---
title: "multiset::key_compare (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::multiset::key_compare"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "key_compare - элемент [STL/CLR]"
ms.assetid: 172c1ac7-fc71-409e-898a-5521eea7201a
caps.latest.revision: 17
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 15
---
# multiset::key_compare (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Порядок делегат для 2 ключей.  
  
## Синтаксис  
  
```  
Microsoft::VisualC::StlClr::BinaryDelegate<GKey, GKey, bool>  
    key_compare;  
```  
  
## Заметки  
 Тип синоним для делегата, определяет порядок ключевых своих аргументов.  
  
## Пример  
  
```  
// cliext_multiset_key_compare.cpp   
// compile with: /clr   
#include <cliext/set>   
  
typedef cliext::multiset<wchar_t> Mymultiset;   
int main()   
    {   
    Mymultiset c1;   
    Mymultiset::key_compare^ kcomp = c1.key_comp();   
  
    System::Console::WriteLine("compare(L'a', L'a') = {0}",   
        kcomp(L'a', L'a'));   
    System::Console::WriteLine("compare(L'a', L'b') = {0}",   
        kcomp(L'a', L'b'));   
    System::Console::WriteLine("compare(L'b', L'a') = {0}",   
        kcomp(L'b', L'a'));   
    System::Console::WriteLine();   
  
// test a different ordering rule   
    Mymultiset c2 = cliext::greater<wchar_t>();   
    kcomp = c2.key_comp();   
  
    System::Console::WriteLine("compare(L'a', L'a') = {0}",   
        kcomp(L'a', L'a'));   
    System::Console::WriteLine("compare(L'a', L'b') = {0}",   
        kcomp(L'a', L'b'));   
    System::Console::WriteLine("compare(L'b', L'a') = {0}",   
        kcomp(L'b', L'a'));   
    return (0);   
    }  
  
```  
  
  **сравнение \(L'a, L'а\) \= false**  
**сравнение \(L'a, L'б\) \= true**  
**сравнение \(L'b, L'а\) \= false**  
**сравнение \(L'a, L'а\) \= false**  
**сравнение \(L'a, L'б\) \= false**  
**сравнение \(L'b, L'а\) \= true**   
## Требования  
 **Заголовок:**\<cliext\/set\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [multiset](../dotnet/multiset-stl-clr.md)   
 [multiset::key\_comp](../Topic/multiset::key_comp%20\(STL-CLR\).md)   
 [multiset::key\_type](../dotnet/multiset-key-type-stl-clr.md)   
 [multiset::value\_compare](../Topic/multiset::value_compare%20\(STL-CLR\).md)