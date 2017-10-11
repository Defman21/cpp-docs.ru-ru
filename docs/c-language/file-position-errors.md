---
title: "Ошибки положения в файле | Документация Майкрософт"
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
- file pointers [C++], file position errors
ms.assetid: d5e59d8b-08c0-4927-a338-0b2d8234ce24
caps.latest.revision: 6
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 16d1bf59dfd4b3ef5f037aed9c0f6febfdf1a2e8
ms.openlocfilehash: ebbb6ab903db73fce84059af567dd5e80dfb3afb
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="file-position-errors"></a>Ошибки позиции файла
**ANSI 4.9.9.1, 4.9.9.4** Значение, задаваемое макросу `errno` функциями `fgetpos` и `ftell` при ошибке  
  
 В случае сбоя функции `fgetpos` или `ftell` для макроса `errno` задается значение константы `EINVAL` из манифеста, если недопустима позиция, или значение EBADF, если недопустим номер файла. Эти константы определены в файле ERRNO.H.  
  
## <a name="see-also"></a>См. также  
 [Функции библиотеки](../c-language/library-functions.md)