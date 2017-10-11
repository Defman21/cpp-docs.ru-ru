---
title: "Ошибка компилятора C3809 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C3809
dev_langs:
- C++
helpviewer_keywords:
- C3809
ms.assetid: 37eca584-c20c-464e-8e45-a987214b7ce4
caps.latest.revision: 9
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: e68e6f3b1309a0135b439bfe8f3f067a0c90a6ac
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3809"></a>Ошибка компилятора C3809
class: управляемый тип или тип WinRT не может иметь дружественные функции, классы и интерфейсы  
  
 Управляемые типы и типы среды выполнения Windows не могут иметь дружественные элементы. Чтобы устранить эту ошибку, не объявляйте дружественные элементы внутри управляемых или типов среды выполнения Windows.  
  
 Следующий пример приводит к возникновению ошибки C3809:  
  
```  
// C3809a.cpp  
// compile with: /clr  
ref class A {};  
  
ref class B  
{  
public:  
   friend ref class A;   // C3809  
};  
  
int main()  
{  
}  
```