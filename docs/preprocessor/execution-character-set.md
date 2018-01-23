---
title: "кодировка_выполнения | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp
- devlang-cpp
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- execution_character_set
- vc-pragma.execution_character_set
dev_langs: C++
helpviewer_keywords: pragma execution_character_set
ms.assetid: 32248cbc-7c92-4dca-8442-230c052b53ad
caps.latest.revision: "3"
author: corob-msft
ms.author: corob
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: f1064f5cf97ba6b919e718c60c8346e86d643ced
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="executioncharacterset"></a>кодировка_выполнения
Указывает набор символов исполнения, используемый для строковых и символьных литералах. Эта директива не требуется для литералов, помеченные с префиксом u8.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
#pragma execution_character_set("target")  
```  
  
#### <a name="parameters"></a>Параметры  
 `target`  
 Указывает набор символов исполнения целевой. В настоящее время только выполнение целевых объектов в набор, поддерживаемый в «utf-8».  
  
## <a name="remarks"></a>Примечания  
 Эта директива компилятора является устаревшим, начиная с Visual Studio 2015 с обновлением 2. Мы рекомендуем использовать **/execution-charset:utf-8** или **/UTF-8** параметры компилятора, а также с помощью `u8` префикс на узкие символьные и строковые литералы, содержащие расширенных символы. Дополнительные сведения о `u8` префикса см. в разделе [строковые и символьные литералы](../cpp/string-and-character-literals-cpp.md). Дополнительные сведения о параметрах компилятора см. в разделе [(задать выполнение кодировки) / Execution-CharSet](../build/reference/execution-charset-set-execution-character-set.md) и [/UTF-8 (задать источник и исполняемый файл кодировки UTF-8)](../build/reference/utf-8-set-source-and-executable-character-sets-to-utf-8.md).  
  
 `#pragma execution_character_set("utf-8")` Директива указывает компилятору кодирования узких символов и узкие строковые литералы в исходном коде как UTF-8 в исполняемом файле. Кодирование вывода не зависит от исходного файла кодировку.  
  
 По умолчанию компилятор кодирует обычных символов и строку обычных символов с помощью текущей кодовой странице как набор символов исполнения. Это означает, что Юникода или кодировку DBCS в литерале запрещенные символы вне диапазона текущей кодовой странице преобразуются в символ замены по умолчанию в выходных данных. Юникод и DBCS символов усекаются до их младший байт. Это почти наверняка не как предполагалось. Можно указать кодировку UTF-8 для литералов в исходном файле, с помощью `u8` префикс. Компилятор передает эти строки в кодировке UTF-8 на выходе. Узкие символьные литералы префиксом u8 должны помещаться в один байт или они усекаются в выходных данных.  
  
 По умолчанию Visual Studio использует текущую кодовую страницу как источника кодировку, используемую для интерпретации исходный код для вывода. При чтении файла Visual Studio интерпретирует его согласно текущей кодовой странице, если было задано кодовую страницу файла или метку порядка байтов (BOM) UTF-16 символов обнаружены или, в начале файла. Так как UTF-8 не может быть назначена текущей кодовой странице, когда автоматическое обнаружение обнаруживает исходных файлов в кодировке UTF-8 без отметки BOM, Visual Studio предполагается, они кодируются с помощью текущей кодовой страницы. Символы в исходном файле, которые находятся вне диапазона указанного или автоматически обнаружил, что может привести к кодовой странице из-за ошибки и предупреждения компилятора.  
  
## <a name="see-also"></a>См. также  
 [Директивы pragma и ключевое слово __Pragma](../preprocessor/pragma-directives-and-the-pragma-keyword.md)   
 [/ Execution-CharSet (задать выполнение кодировки)](../build/reference/execution-charset-set-execution-character-set.md)   
 [/ UTF-8 (задать источник и исполняемый объект кодировки UTF-8)](../build/reference/utf-8-set-source-and-executable-character-sets-to-utf-8.md)