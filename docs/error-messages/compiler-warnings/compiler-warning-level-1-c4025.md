---
title: "Предупреждение (уровень 1) C4025 компилятора | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C4025
dev_langs:
- C++
helpviewer_keywords:
- C4025
ms.assetid: c4f6a651-0641-4446-973e-8290065e49ad
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 0e9bca6428358d1ce33e8069c7fcdfef19b23c7a
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-warning-level-1-c4025"></a>Предупреждение компилятора (уровень 1) C4025
"число": относительный указатель передан в функцию с аргументами-переменными: параметр <номер>  
  
 Передача относительного указателя в функцию с аргументами-переменными нормализует указатель с непредвиденными результатами. Не передавайте относительные указатели в функции с аргументами-переменными.