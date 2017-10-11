---
title: "Класс gslice_array | Документы Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- valarray/std::gslice_array
dev_langs:
- C++
helpviewer_keywords:
- gslice_array class
ms.assetid: ad1b4514-b14a-4baf-a293-d5a8e8674c75
caps.latest.revision: 20
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 65f4e356ad0d46333b0d443d0fd6ac0b9f2b6f58
ms.openlocfilehash: 47dd54524e0a99cb2e725a10b1125c5a022a74d5
ms.contentlocale: ru-ru
ms.lasthandoff: 10/03/2017

---
# <a name="gslicearray-class"></a>Класс gslice_array
Внутренний, вспомогательный класс шаблона, который поддерживает общие объекты срезов, предоставляя операции между массивами подмножеств, заданные общим срезом valarray.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
template <class Type>  
class gslice_array : public gsplice {  
public:  
    typedef Type value_type;  
    void operator=(const valarray<Type>& x) const;

 
 
    void operator=(const Type& x) const;

 
 
    void operator*=(const valarray<Type>& x) const;

 
 
    void operator/=(const valarray<Type>& x) const;

 
 
    void operator%=(const valarray<Type>& x) const;

 
 
    void operator+=(const valarray<Type>& x) const;

 
 
    void operator-=(const valarray<Type>& x) const;

 
 
    void operator^=(const valarray<Type>& x) const;

 
 
    void operator&=(const valarray<Type>& x) const;

 
 
    void operator|=(const valarray<Type>& x) const;

 
 
    void operator<<=(const valarray<Type>& x) const;

 
 
    void operator>>=(const valarray<Type>& x) const;

 
 
// The rest is private or implementation defined  
}  
```  
  
## <a name="remarks"></a>Примечания  
 Класс описывает объект, который хранит ссылку на объект **va** класса [valarray](../standard-library/valarray-class.md)**\<Type>**, вместе с объектом **gs** класса [gslice](../standard-library/gslice-class.md), который описывает последовательность элементов для выбора из объекта **valarray\<Type>**.  
  
 Объект **gslice_array\<Type>** создается только путем написания выражения вида [va&#91;gs&#93;](../standard-library/valarray-class.md#op_at). После этого функции-члены класса gslice_array ведут себя как соответствующие сигнатуры функций, заданные для **valarray\<Type>** с той разницей, что затрагивается только последовательность выбранных элементов.  
  
 Класс шаблона создается неявно с помощью определенных операций valarray и не может использоваться непосредственно в программе. Вместо этого оператором индекса среза используется внутренний вспомогательный класс шаблона:  
  
 `gslice_array`\< **Type**> `valarray`\< **Type**>:: `operator[]` ( **constgslice&**).  
  
 Объект **gslice_array\<Type>** создается только путем написания выражения вида **va[gsl]** для среза **gsl** класса valarray **va**. После этого функции-члены класса gslice_array ведут себя как соответствующие сигнатуры функций, заданные для **valarray\<Type>** с той разницей, что затрагивается только последовательность выбранных элементов. Последовательность, управляемая классом gslice_array, определяется тремя параметрами конструктора среза: индексом первого элемента в первом срезе, количеством элементов в каждом срезе и расстояние между элементами в каждом срезе.  
  
 В следующем примере:  
  
```  
const size_t lv[] = {2, 3};  
const size_t dv[] = {7, 2};  
const valarray<size_t> len(lv, 2), str(dv, 2);

// va[gslice(3, len, str)] selects elements with  
//   indices 3, 5, 7, 10, 12, 14  
```  
  
 Чтобы процедура была действительной, индексы должны быть действительными.  
  
## <a name="example"></a>Пример  
 Пример объявления и использования класса slice_array см. в разделе [gslice::gslice](../standard-library/gslice-class.md#gslice).  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** \<valarray>  
  
 **Пространство имен:** std  
  
## <a name="see-also"></a>См. также  
 [Потокобезопасность в стандартной библиотеке C++](../standard-library/thread-safety-in-the-cpp-standard-library.md)

