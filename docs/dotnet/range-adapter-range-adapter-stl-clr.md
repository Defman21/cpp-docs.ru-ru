---
title: "range_adapter::range_adapter (STL/CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "cliext::range_adapter::range_adapter"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "range_adapter - элемент [STL/CLR]"
ms.assetid: b16af13f-3358-4e82-927d-d0d4986bcb18
caps.latest.revision: 9
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 7
---
# range_adapter::range_adapter (STL/CLR)
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Создает объект адаптера.  
  
## Синтаксис  
  
```  
range_adapter();  
range_adapter(range_adapter<Iter>% right);  
range_adapter(range_adapter<Iter>^ right);  
range_adapter(Iter first, Iter last);  
```  
  
#### Параметры  
 first  
 Первый итератор, создающееся.  
  
 last  
 Второй итератор, создающееся.  
  
 правый  
 Объект, подлежащих копированию.  
  
## Заметки  
 Конструктор:  
  
 `range_adapter();`  
  
 инициализирует сохраненного пары итератора с итераторами построенными\).  
  
 Конструктор:  
  
 `range_adapter(range_adapter<Iter>% right);`  
  
 инициализирует сохраненного пары итератора, скопировав пары, хранящиеся в `right`.  
  
 Конструктор:  
  
 `range_adapter(range_adapter<Iter>^ right);`  
  
 инициализирует сохраненного пары итератора, скопировав пары, хранящиеся в `*right`.  
  
 Конструктор:  
  
 `range_adapter(Iter^ first, last);`  
  
 инициализирует сохраненного пары итератора с `first` и `last`.  
  
## Пример  
  
```  
// cliext_range_adapter_construct.cpp   
// compile with: /clr   
#include <cliext/adapter>   
#include <cliext/deque>   
  
typedef cliext::deque<wchar_t> Mycont;   
typedef cliext::range_adapter<Mycont::iterator> Myrange;   
int main()   
    {   
    cliext::deque<wchar_t> d1;   
    d1.push_back(L'a');   
    d1.push_back(L'b');   
    d1.push_back(L'c');   
  
// construct an empty adapter   
    Myrange c1;   
  
// construct with an iterator pair   
    Myrange c2(d1.begin(), d1.end());   
    for each (wchar_t elem in c2)   
        System::Console::Write(" {0}", elem);   
    System::Console::WriteLine();   
  
// construct by copying another adapter   
    Myrange c3(c2);   
    for each (wchar_t elem in c3)   
        System::Console::Write(" {0}", elem);   
    System::Console::WriteLine();   
  
// construct by copying an adapter handle   
    Myrange c4(%c3);   
    for each (wchar_t elem in c4)   
        System::Console::Write(" {0}", elem);   
    System::Console::WriteLine();   
  
    return (0);   
    }  
  
```  
  
  **a b c**  
 **a b c**  
 **a b c**   
## Требования  
 **Заголовок:**\<cliext\/adapter\>  
  
 **Пространство имен:** cliext  
  
## См. также  
 [range\_adapter](../dotnet/range-adapter-stl-clr.md)   
 [range\_adapter::operator\=](../dotnet/range-adapter-operator-assign-stl-clr.md)