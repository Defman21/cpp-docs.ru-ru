---
title: "Маркеры (C++) | Документы Microsoft"
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
- tokens [C++]
- parsing, C++ tokens
- translation units
- white space, in C++ tokens
ms.assetid: aa812fd0-6d47-4f3f-aee0-db002ee4d8b9
caps.latest.revision: 7
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: 041750d86f12f82e0f905c65f0a75d6a32f37cdf
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="tokens-c"></a>Маркеры (C++)
Токен — это наименьший элемент на C++, который имеет значение для компилятора. Синтаксический анализатор C++ распознает следующие типы токенов: идентификаторы, ключевые слова, литералы, операторы, символы пунктуации и другие разделители. Поток этих токенов составляет один блок трансляции.  
  
 Токены обычно разделяются *символами-разделителями*. Возможны следующие символы-разделители:  
  
-   Пробелы  
  
-   Символы горизонтальной и вертикальной табуляции  
  
-   Символы перевода строки  
  
-   Символы перевода страницы  
  
-   Комментарии  
  
 Средство синтаксического анализа распознает ключевые слова, идентификаторы, литералы, операторы и символы пунктуации. Сведения о конкретных типах токенов см. в разделах [Ключевые слова](../cpp/keywords-cpp.md), [Идентификаторы](../cpp/identifiers-cpp.md), [Числовые, логические литералы и литералы-указатели](../cpp/numeric-boolean-and-pointer-literals-cpp.md), [Строковые и символьные литералы](../cpp/string-and-character-literals-cpp.md), [Определяемые пользователем литералы](../cpp/user-defined-literals-cpp.md), [Встроенные операторы C++, приоритет и ассоциативность](../cpp/cpp-built-in-operators-precedence-and-associativity.md)и [Символы пунктуации](../cpp/punctuators-cpp.md). Символы-разделители игнорируются, если только они не требуются для разделения токенов.  
  
 Токены предварительной обработки используются на этапах предварительной обработки для создания потока лексем, передаваемого в компилятор. Категории токенов предварительной обработки включают имена заголовков, идентификаторы, числа предварительной обработки, символьные литералы, строковые литералы, операторы предварительной обработки и символы пунктуации, а также одиночные символы, не являющиеся пробелами, которые не попадают ни в одну из других категорий. Символьные и строковые литералы могут быть литералами, определенными пользователем. Токены предварительной обработки могут разделяться символами-разделителями или комментариями.  
  
 Анализатор отделяет токены из входного потока путем создания самого длинного из возможных токенов, сканируя входные символы слева направо. Рассмотрим следующий фрагмент кода:  
  
```  
a = i+++j;  
```  
  
 Программист, который записывал этот код, мог намереваться использовать один из следующих двух операторов:  
  
```  
a = i + (++j)  
  
a = (i++) + j  
```  
  
 Поскольку синтаксический анализатор создает из входного потока самый длинный из возможных токенов, он выбирает вторую интерпретацию, создавая токены `i++`, `+`и `j`.  
  
## <a name="see-also"></a>См. также  
 [Лексические соглашения](../cpp/lexical-conventions.md)