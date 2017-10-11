---
title: "Диагностические сведения, выводимые функцией assert | Документация Майкрософт"
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
ms.assetid: 78b64200-520d-40da-9a61-71553f411d4f
caps.latest.revision: 6
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 16d1bf59dfd4b3ef5f037aed9c0f6febfdf1a2e8
ms.openlocfilehash: d6e5ea4e5f8bae3fda190ac7a7136035aea0c948
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="diagnostic-printed-by-the-assert-function"></a>Диагностика, напечатанная функцией assert
**ANSI 4.2** Диагностика, выведенная функцией assert, и поведение завершения функции **assert**  
  
 Функция **assert** выводит диагностическое сообщение и вызывает подпрограмму **abort**, если значение выражения — false (0). Диагностическое сообщение имеет форму  
  
 **Assertion failed**: *expression***, file** *filename***, line** *linenumber*  
  
 где имя файла — это имя файла исходного кода, а номер строки — это номер строки утверждения, завершившегося сбоем в файле исходного кода. Если выражение равно true (ненулевое), никакие действия не предпринимаются.  
  
## <a name="see-also"></a>См. также  
 [Функции библиотеки](../c-language/library-functions.md)