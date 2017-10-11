---
title: "Символы поля типа scanf | Документация Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
apilocation:
- msvcr90.dll
- msvcr80.dll
- msvcr100.dll
- msvcr110_clr0400.dll
- msvcr110.dll
- msvcr120.dll
apitype: DLLExport
f1_keywords:
- scanf
dev_langs:
- C++
helpviewer_keywords:
- scanf function, type field characters
ms.assetid: 5d546a84-715b-44ca-b1c5-bbe997f9ff62
caps.latest.revision: 21
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: Human Translation
ms.sourcegitcommit: d6eb43b2e77b11f4c85f6cf7e563fe743d2a7093
ms.openlocfilehash: 82ace58042dd9c7f9cceb0ef0781968532ae7b29
ms.contentlocale: ru-ru
ms.lasthandoff: 05/18/2017

---
# <a name="scanf-type-field-characters"></a>Символы поля типа scanf
Следующие сведения применимы к любой функции из семейства `scanf` , включая безопасные версии, например `scanf_s`.  
  
 Символ `type` — единственное обязательное поле формата; он находится после всех необязательных полей формата. Символ `type` определяет, интерпретируется ли аргумент как символ, строка или число.  
  
### <a name="type-characters-for-scanf-functions"></a>Символы типа для функций scanf  
  
|Знак|Ожидаемый тип входных данных|Тип аргумента|Аргумент размера в безопасной версии?|  
|---------------|----------------------------|----------------------|--------------------------------------|  
|`c`|Символ. При использовании с функциями `scanf` определяет однобайтовый символ; при использовании с функциями `wscanf` определяет расширенный символ. Символы-разделители обычно пропускаются при чтении, если указано значение `c` . Для считывания следующего однобайтового символа, отличного от пробельного, используйте `%1s`; для считывания следующего расширенного символа, отличного от пробельного, используйте `%1ws`.|Указатель на `char` при использовании с функциями `scanf` , указатель на `wchar_t` при использовании с функциями `wscanf` .|Обязательный. Размер не учитывает пространство для завершающего нуль-символа.|  
|`C`|Символ противоположного размера. При использовании с функциями `scanf` определяет расширенный символ; при использовании с функциями `wscanf` определяет однобайтовый символ. Символы-разделители обычно пропускаются при чтении, если указано значение `C` . Для считывания следующего однобайтового символа, отличного от пробельного, используйте `%1s`; для считывания следующего расширенного символа, отличного от пробельного, используйте `%1ws`.|Указатель на `wchar_t` при использовании с функциями `scanf` , указатель на `char` при использовании с функциями `wscanf` .|Обязательный. Аргумент размера не учитывает пространство для завершающего нуль-символа.|  
|`d`|Десятичное целое число.|Указатель на `int`.|Нет.|  
|`i`|Значение типа integer. Шестнадцатеричное число, если входная строка начинается с "0x" или "0X", восьмеричное число, если строка начинается с "0"; в противном случае — десятичное число.|Указатель на `int`.|Нет.|  
|`o`|Восьмеричное целое число.|Указатель на `int`.|Нет.|  
|`p`|Адрес указателя в шестнадцатеричном виде. Максимальное число считываемых цифр зависит от размера указателя (32- или 64-разрядный), который определяется архитектурой компьютера. "0x" и "0X" принимаются как префиксы.|Указатель на `void*`.|Нет.|  
|`u`|Десятичное целое число без знака.|Указатель на `unsigned int`.|Нет.|  
|`x`|Шестнадцатеричное целое число.|Указатель на `int`.|Нет.|  
|`e`, `E`, `f`, `F`, `g`, `G`|Число с плавающей запятой, состоящее из необязательного знака (+ или –), последовательности из одной или нескольких десятичных цифр, содержащей десятичную запятую, и необязательной экспоненты ("e" или "E"), за которой следует целое число со знаком (необязательным).|Указатель на `float`.|Нет.|  
|`a`, `A`|Значение с плавающей запятой, состоящее из последовательности один или нескольких шестнадцатеричных цифр, содержащее дополнительную десятичную запятую, и экспонента ("p" или "P"), за которой идет десятичное значение.|Указатель на `float`.|Нет.|  
|`n`|Нет данных, прочитанных из потока или буфера.|Указатель на `int`, по которому сохраняется число символов, успешно прочитанных из потока или буфера до этой точки в текущем вызове функции `scanf` или `wscanf` .|Нет.|  
|`s`|Строка, до первого символа-разделителя (пробела, знака табуляции или новой строки). Для чтения строк, не разделенных символами-разделителями, используйте пару квадратных скобок (`[ ]`), как описано в разделе [scanf Width Specification](../c-runtime-library/scanf-width-specification.md).|При использовании с функциями `scanf` обозначает массив однобайтовых символов; при использовании с функциями `wscanf` обозначает массив расширенных символов. В любом случае массив символов должен быть достаточно большим для поля ввода и автоматически добавляемого завершающего нуль-символа.|Обязательный. Размер включает место для завершающего нуль-символа.|  
|`S`|Строка символов противоположного размера, до первого символа-разделителя (пробела, знака табуляции или новой строки). Для чтения строк, не разделенных символами-разделителями, используйте пару квадратных скобок (`[ ]`), как описано в разделе [scanf Width Specification](../c-runtime-library/scanf-width-specification.md).|При использовании с функциями `scanf` обозначает массив расширенных символов; при использовании с функциями `wscanf` обозначает массив однобайтовых символов. В любом случае массив символов должен быть достаточно большим для поля ввода и автоматически добавляемого завершающего нуль-символа.|Обязательный. Размер включает место для завершающего нуль-символа.|  
  
  
 Аргументы размера, при необходимости, необходимо передавать в списке параметров сразу после аргумента, к которому они применяются. Например, приведенный ниже код  
  
```  
char string1[11], string2[9];  
scanf_s("%10s %8s", string1, 11, string2, 9);  
```  
  
 считывает строку с максимальной длиной 10 в `string1`и строку с максимальной длиной 8 в `string2`. Размер буфера должен быть по крайней мере на один больше указанной ширины, поскольку должно быть зарезервировано место для завершающего нуль-символа.  
  
 Строка формата может обрабатывать однобайтовые или расширенные входные символы независимо от того, используется ли однобайтовая или расширенная версия функции. Таким образом, для чтения однобайтовых или расширенных символов с использованием функций `scanf` и `wscanf` используйте описатели формата следующим образом.  
  
|Чтобы считать символ как|Используйте эту функцию|С этими описателями формата|  
|--------------------------|-----------------------|----------------------------------|  
|один байт|Функции`scanf` |`c`, `hc`или `hC`|  
|один байт|Функции`wscanf` |`C`, `hc`или `hC`|  
|расширенный символ|Функции`wscanf` |`c`, `lc`или `lC`|  
|расширенный символ|Функции`scanf` |`C`, `lc`или `lC`|  
  
 Для чтения строк с использованием функций `scanf` и `wscanf` используйте указанную выше таблицу с описателями формата `s` и `S` вместо `c` и `C`.  
  
## <a name="see-also"></a>См. также  
 [scanf, _scanf_l, wscanf, _wscanf_l](../c-runtime-library/reference/scanf-scanf-l-wscanf-wscanf-l.md)