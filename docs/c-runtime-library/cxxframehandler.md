---
title: "__CxxFrameHandler | Документация Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- __CxxFrameHandler
apilocation:
- msvcr110.dll
- msvcrt.dll
- msvcr80.dll
- msvcr100.dll
- msvcr110_clr0400.dll
- msvcr90.dll
- msvcr120.dll
apitype: DLLExport
f1_keywords:
- __CxxFrameHandler
dev_langs:
- C++
helpviewer_keywords:
- __CxxFrameHandler
ms.assetid: b79ac97f-425a-42ae-9b91-8beaef935333
caps.latest.revision: 3
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 16d1bf59dfd4b3ef5f037aed9c0f6febfdf1a2e8
ms.openlocfilehash: 75f900560f226557bc160bdf74df4467b0c7aa32
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="cxxframehandler"></a>__CxxFrameHandler
Внутренняя функция CRT. Используется CRT для обработки кадров структурированной обработки исключений.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
EXCEPTION_DISPOSITION __CxxFrameHandler(  
      EHExceptionRecord  *pExcept,  
      EHRegistrationNode *pRN,  
      void               *pContext,   
      DispatcherContext  *pDC  
   )  
```  
  
#### <a name="parameters"></a>Параметры  
 `pExcept`  
 Запись исключения, передаваемая в возможные операторы `catch`.  
  
 `pRN`  
 Динамические сведения о кадре стека, который используется для обработки исключения. Дополнительные сведения см. в описании ehdata.h.  
  
 `pContext`  
 Контекст. (Не используется для процессоров Intel.)  
  
 `pDC`  
 Дополнительные сведения о входе в функцию и кадре стека.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Одно из значений *выражения фильтра*, используемое в [операторе try-except](../cpp/try-except-statement.md).  
  
## <a name="remarks"></a>Примечания  
  
## <a name="requirements"></a>Требования  
  
|Подпрограмма|Обязательный заголовок|  
|-------------|---------------------|  
|__CxxFrameHandler|excpt.h, ehdata.h|