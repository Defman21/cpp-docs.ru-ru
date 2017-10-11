---
title: "_bstr_t::Detach | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- _bstr_t::Detach
dev_langs:
- C++
helpviewer_keywords:
- Detach method [C++]
ms.assetid: cc8284bd-f68b-4fff-b2e6-ce8354dabf8b
caps.latest.revision: 6
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: 2bdc40741ab10ac180742a1e310285290daa08c6
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="bstrtdetach"></a>_bstr_t::Detach
**Блок, относящийся только к системам Майкрософт**  
  
 Возвращает строку `BSTR`, инкапсулированную объектом `_bstr_t`, и отсоединяет ее (`BSTR`) от этого объекта (`_bstr_t`).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
BSTR Detach( ) throw;  
  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 `BSTR` в оболочке `_bstr_t`.  
  
## <a name="example"></a>Пример  
 В разделе [_bstr_t::Assign](../cpp/bstr-t-assign.md) пример использования **отсоединения**.  
  
 **Завершение блока, относящегося только к системам Майкрософт**  
  
## <a name="see-also"></a>См. также  
 [_bstr_t Class](../cpp/bstr-t-class.md)