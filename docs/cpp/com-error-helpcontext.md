---
title: "_com_error::HelpContext | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- _com_error::HelpContext
dev_langs:
- C++
helpviewer_keywords:
- HelpContext method [C++]
ms.assetid: 160d6443-9b68-4cf5-a540-50da951a5b2b
caps.latest.revision: 6
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: d3eb0678e7d3b7cb4c1824cf17bc25499bf0c0ce
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="comerrorhelpcontext"></a>_com_error::HelpContext
**Блок, относящийся только к системам Майкрософт**  
  
 Вызовы **IErrorInfo::GetHelpContext** функции.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DWORD HelpContext( ) const throw( );  
  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращает результат **IErrorInfo::GetHelpContext** для **IErrorInfo** записанного в `_com_error` объекта. Если не **IErrorInfo** объекта записан, возвращается нулевое значение.  
  
## <a name="remarks"></a>Примечания  
 Любые сбои при вызове **IErrorInfo::GetHelpContext** метод игнорируется.  
  
 **Завершение блока, относящегося только к системам Майкрософт**  
  
## <a name="see-also"></a>См. также  
 [Класс _com_error](../cpp/com-error-class.md)