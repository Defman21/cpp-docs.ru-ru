---
title: "Функции CRT, которые не поддерживаются средой выполнения Windows | Документация Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- unsupported CRT functions, Windows Runtime
- Windows Runtime, unsupported CRT functions
ms.assetid: bb8386d6-0ef8-460c-88d8-addff009b6f1
caps.latest.revision: 14
author: corob-msft
ms.author: corob
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 0eb057f9d229c659f339f996d1ff38f65fd2e018
ms.openlocfilehash: be461857f4aa1625094b20a2241ab15853d2aa81
ms.contentlocale: ru-ru
ms.lasthandoff: 06/01/2017

---
# <a name="windows-runtime-unsupported-crt-functions"></a>Функции CRT, которые не поддерживаются средой выполнения Windows
Многие API среды выполнения C (CRT) не могут использоваться в приложениях [!INCLUDE[win8_appname_long](../build/includes/win8_appname_long_md.md)], выполняемых в среде выполнения Windows. Для сборки таких приложений используется флаг компилятора /ZW. Список неподдерживаемых функций CRT см. в статье [CRT functions not supported in Universal Windows Platform apps](http://msdn.microsoft.com/library/windows/apps/jj606124.aspx) (Функции CRT, которые не поддерживаются приложениями универсальной платформы Windows).  
  
 Все API CRT описаны в документации в статье [CRT Alphabetical Function Reference](../c-runtime-library/reference/crt-alphabetical-function-reference.md) (Алфавитный указатель функций CRT).  
  
## <a name="see-also"></a>См. также  
 [Процедуры среды выполнения по категориям](../c-runtime-library/run-time-routines-by-category.md)   
 [Алфавитный указатель функций](../c-runtime-library/reference/crt-alphabetical-function-reference.md)