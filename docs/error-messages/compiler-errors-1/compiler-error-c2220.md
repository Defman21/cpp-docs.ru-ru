---
title: "Ошибка компилятора C2220 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- C2220
dev_langs:
- C++
helpviewer_keywords:
- C2220
ms.assetid: d610802c-64d7-40ad-a2a6-0ed0b6815a6c
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: dc31519b2153c66ea9bab42f536ba7c6be5b2a10
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="compiler-error-c2220"></a>Ошибка компилятора C2220
Предупреждение, обрабатываемое как ошибка, объектный файл не создан  
  
 [/ WX](../../build/reference/compiler-option-warning-level.md) указывает компилятору обрабатывать все предупреждения как ошибки. Из-за ошибки, объект или исполняемый файл был создан.  
  
 Эта ошибка появляется, только когда **/WX** установлен флаг и возникновении предупреждения во время компиляции. Чтобы устранить эту ошибку, необходимо исключить каждое из них в проекте.  
  
### <a name="to-fix-use-one-of-the-following-techniques"></a>Чтобы устранить проблему, используйте один из следующих способов  
  
-   Устранение проблем, которые выводят предупреждения в проекте.  
  
-   На более низком уровне предупреждений компиляции — например, использовать **/W3** вместо **/W4**.  
  
-   Используйте [предупреждение](../../preprocessor/warning.md) pragma, чтобы отключить или запретить конкретное предупреждение.  
  
-   Не используйте **/WX** для компиляции.