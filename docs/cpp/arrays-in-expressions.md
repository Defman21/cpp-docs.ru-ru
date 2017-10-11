---
title: "Массивы в выражениях | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- C++
helpviewer_keywords:
- expressions [C++], arrays in
- arrays [C++], in expressions
ms.assetid: 6e5a795b-d6bd-4e39-b313-6a20d47c4d4b
caps.latest.revision: 7
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: ec97fba837ffae0a03ff8d4fc3d85c4011aa59c6
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="arrays-in-expressions"></a>Массивы в выражениях
При идентификатор типа массива находится в выражении, отличный от `sizeof`, взятия адреса (**&**), или инициализации ссылки, он преобразуется в указатель на первый элемент массива. Пример:  
  
```  
char szError1[] = "Error: Disk drive not ready.";  
char *psz = szError1;  
```  
  
 Указатель `psz` указывает на первый элемент массива `szError1`. Обратите внимание, что массивы, в отличие от указателей, не являются изменяемыми l-значениями. Таким образом, следующее присвоение незаконно.  
  
```  
szError1 = psz;  
```  
  
## <a name="see-also"></a>См. также  
 [Массивы](../cpp/arrays-cpp.md)