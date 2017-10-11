---
title: "Практическое руководство. Перебор элементов универсальной коллекции с использованием цикла for each | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "reference"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "универсальная коллекция, итерация через"
ms.assetid: 00288d53-3d41-44d0-be5b-b3033456ceaa
caps.latest.revision: 13
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 11
---
# Практическое руководство. Перебор элементов универсальной коллекции с использованием цикла for each
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Функция [Универсальные шаблоны](../windows/generics-cpp-component-extensions.md) Visual C\+\+ позволяет создать универсальные коллекции.  
  
## Пример  
 В этом образце показано, как использовать `for each` с простой универсальной коллекции типа значения.  
  
```  
// for_each_generics.cpp  
// compile with: /clr  
using namespace System;  
using namespace System::Collections::Generic;  
  
generic <class T>  
public value struct MyArray : public IEnumerable<T> {     
  
   MyArray( array<T>^ d ) {  
      data = d;  
   }  
  
   ref struct enumerator : IEnumerator<T> {  
      enumerator( MyArray^ myArr ) {  
         colInst = myArr;  
         currentIndex = -1;  
      }  
  
      virtual bool MoveNext() = IEnumerator<T>::MoveNext {  
         if ( currentIndex < colInst->data->Length - 1 ) {  
            currentIndex++;  
            return true;  
         }  
  
         return false;  
      }  
  
      virtual property T Current {  
         T get() {  
            return colInst->data[currentIndex];  
         }  
      };  
  
      property Object^ CurrentNonGeneric {  
         virtual Object^ get() = System::Collections::IEnumerator::Current::get {  
            return colInst->data[currentIndex];  
         }  
      };  
  
      virtual void Reset() {}  
      ~enumerator() {}  
  
      MyArray^ colInst;  
      int currentIndex;  
   };  
  
   array<T>^ data;  
  
   virtual IEnumerator<T>^ GetEnumerator() {  
      return gcnew enumerator(*this);  
   }  
   virtual System::Collections::IEnumerator^ GetEnumeratorNonGeneric() = System::Collections::IEnumerable::GetEnumerator {  
      return gcnew enumerator(*this);  
   }  
};  
  
int main() {  
   MyArray<int> col = MyArray<int>( gcnew array<int>{10, 20, 30 } );  
  
   for each ( Object^ c in col )  
      Console::WriteLine((int)c);  
}  
```  
  
  **10**  
**20**  
**30**   
## См. также  
 [for each, in](../dotnet/for-each-in.md)