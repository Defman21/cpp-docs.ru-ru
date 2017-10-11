---
title: "Класс is_copy_assignable | Документы Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- type_traits/std::is_copy_assignable
dev_langs:
- C++
helpviewer_keywords:
- is_copy_assignable
ms.assetid: 3ae6bca1-85fb-4829-9ee9-0183b081ff50
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 65f4e356ad0d46333b0d443d0fd6ac0b9f2b6f58
ms.openlocfilehash: eeb83c55fbb83597c0e7a17cc484ae0a02e1f740
ms.contentlocale: ru-ru
ms.lasthandoff: 10/03/2017

---
# <a name="iscopyassignable-class"></a>Класс is_copy_assignable
Проверяет, может ли тип быть скопирован при присвоении значения.  
  
## <a name="syntax"></a>Синтаксис  
  
```
template <class Ty>
struct is_copy_assignable;
```  
  
#### <a name="parameters"></a>Параметры  
 `Ty`  
 Запрашиваемый тип.  
  
## <a name="remarks"></a>Примечания  
 Экземпляр предиката типа содержит значение true, если тип `Ty` является классом, имеющим оператор присваивания копированием, в противном случае — значение false. Эквивалентно is_assignable\<Ty&, const Ty&>.  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** \<type_traits>  
  
 **Пространство имен:** std  
  
## <a name="see-also"></a>См. также  
 [<type_traits>](../standard-library/type-traits.md)



