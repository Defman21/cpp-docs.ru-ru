---
title: "Класс is_move_assignable | Документы Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- type_traits/std::is_move_assignable
dev_langs:
- C++
helpviewer_keywords:
- is_move_assignable
ms.assetid: f33137f2-0639-4912-8745-bc0f9fd18d28
caps.latest.revision: 13
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 65f4e356ad0d46333b0d443d0fd6ac0b9f2b6f58
ms.openlocfilehash: 52b30e32afeabe83a79bb32f42ca02936b406d17
ms.contentlocale: ru-ru
ms.lasthandoff: 10/03/2017

---
# <a name="ismoveassignable-class"></a>Класс is_move_assignable
Проверяет, является ли тип присваиваемым при перемещении.  
  
## <a name="syntax"></a>Синтаксис  
  
```
template <class T>
struct is_move_assignable;
```  
  
#### <a name="parameters"></a>Параметры  
 `T`  
 Запрашиваемый тип.  
  
## <a name="remarks"></a>Примечания  
 Тип является тип присваиваемым при перемещении, если ссылку rvalue на тип можно присвоить ссылке на тип. Предикат типа эквивалентен `is_assignable<T&, T&&>`. Присваиваемые при перемещении типы включают ссылочные скалярные типы и типы классов, в которых есть созданные компилятором или определяемые пользователем операторы присваивания перемещением.  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** \<type_traits>  
  
 **Пространство имен:** std  
  
## <a name="see-also"></a>См. также  
 [<type_traits>](../standard-library/type-traits.md)



