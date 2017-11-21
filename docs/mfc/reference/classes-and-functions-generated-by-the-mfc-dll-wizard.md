---
title: "Классы и функции, создаваемые мастером MFC DLL | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- functions [MFC]
- functions [MFC], DLLs
- MFC DLL Wizard
- DLLs [MFC], wizard classes and functions
- classes [MFC], generated by MFC DLL wizard
- code [MFC], generated by MFC DLL wizard
ms.assetid: e69e62fe-4953-42bf-a2fc-50bbf9bdaeaf
caps.latest.revision: "9"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 52465b01b8644b2f4ea1f4a22412af0159e4f598
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="classes-and-functions-generated-by-the-mfc-dll-wizard"></a>Классы и функции, создаваемые мастером MFC DLL
Код, формируемый мастером MFC DLL зависит от типа создаваемой библиотеки DLL и параметры, которые вы выбрали. Мастер библиотек DLL MFC создает тот же код для обоих видов обычные библиотеки DLL MFC.  
  
|Тип библиотеки DLL|Параметр|Классы|Функции|  
|-----------------|------------|-------------|---------------|  
|[Расширение](../../build/extension-dlls-overview.md)|Нет|Нет|`DllMain`|  
|[Обычный](../../build/regular-dlls-dynamically-linked-to-mfc.md)|Нет|Приложение класс, производный от`CWinApp`|Нет|  
|[Обычный](../../build/regular-dlls-dynamically-linked-to-mfc.md)|автоматизация|Приложение класс, производный от`CWinApp`|**DllGetClassObjectDllCanUnloadNowDllRegisterServer**|  
|[Расширение](../../build/extension-dlls-overview.md)|Сокеты окна|Нет|`DllMain`|  
|[Обычный](../../build/regular-dlls-dynamically-linked-to-mfc.md)|Сокеты окна|Приложение класс, производный от`CWinApp`|`InitInstance`содержит вызов`AfxSocketInit`|  
  
## <a name="see-also"></a>См. также  
 [Мастер DLL MFC](../../mfc/reference/mfc-dll-wizard.md)
