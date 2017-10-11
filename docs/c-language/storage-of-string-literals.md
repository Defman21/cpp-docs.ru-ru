---
title: "Хранение строковых литералов | Документация Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- string literals, storage
ms.assetid: ba5e4d2c-d456-44b3-a8ca-354af547ac50
caps.latest.revision: 9
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 16d1bf59dfd4b3ef5f037aed9c0f6febfdf1a2e8
ms.openlocfilehash: 2a1a001899e46fbd8894b72f2c8cd806f1834b7e
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="storage-of-string-literals"></a>Хранение строковых литералов
Символы строкового литерала хранятся по порядку в смежных адресах памяти. Любая escape-последовательность (например, **\\\\** или **\\"**) внутри строкового литерала считается одним символом. В каждый строковый литерал автоматически добавляется нуль-символ (представленный escape-последовательностью **\0**), который обозначает его конец. (Это происходит на [этапе преобразования](../preprocessor/phases-of-translation.md) 7.) Обратите внимание, что компилятор не может сохранить две одинаковые строки отдельно с разными адресами. Ключ [/GF](../build/reference/gf-eliminate-duplicate-strings.md) указывает, что компилятор должен сохранять в исполняемом файле только одну копию одинаковых строк.  
  
## <a name="remarks"></a>Примечания  
 **Блок, относящийся только к системам Майкрософт**  
  
 Строки имеют статическую длительность хранения. Дополнительные сведения о длительности хранения см. в разделе [Классы хранения в C](../c-language/c-storage-classes.md).  
  
 **Завершение блока, относящегося только к системам Майкрософт**  
  
## <a name="see-also"></a>См. также  
 [Строковые литералы в C](../c-language/c-string-literals.md)