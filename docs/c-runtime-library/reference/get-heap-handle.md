---
title: "_get_heap_handle | Документы Майкрософт"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-standard-libraries
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- _get_heap_handle
apilocation:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-heap-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _get_heap_handle
- get_heap_handle
dev_langs:
- C++
helpviewer_keywords:
- heap functions
- memory allocation, heap memory
- _get_heap_handle function
- get_heap_handle function
ms.assetid: a4d05049-8528-494a-8281-a470d1e1115c
caps.latest.revision: 16
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: 2e8c08ed0ccffb7196133de89d4b9588333e1bfa
ms.contentlocale: ru-ru
ms.lasthandoff: 10/09/2017

---
# <a name="getheaphandle"></a>_get_heap_handle
Возвращает дескриптор кучи, используемый системой времени выполнения C.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
intptr_t _get_heap_handle( void );  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращает дескриптор кучи Win32, используемый системой времени выполнения C.  
  
## <a name="remarks"></a>Примечания  
 Используйте эту функцию, чтобы вызвать [HeapSetInformation](http://msdn.microsoft.com/library/windows/desktop/aa366705) и включить кучу низкой фрагментации в куче CRT.  
  
## <a name="requirements"></a>Требования  
  
|Подпрограмма|Обязательный заголовок|  
|-------------|---------------------|  
|`_get_heap_handle`|\<malloc.h>|  
  
 Дополнительные сведения о совместимости см. в разделе [Совместимость](../../c-runtime-library/compatibility.md).  
  
## <a name="sample"></a>Пример  
  
```  
// crt_get_heap_handle.cpp  
// compile with: /MT  
#include <windows.h>  
#include <malloc.h>  
#include <stdio.h>  
  
int main(void)  
{  
    intptr_t hCrtHeap = _get_heap_handle();  
    ULONG ulEnableLFH = 2;  
    if (HeapSetInformation((PVOID)hCrtHeap,  
                           HeapCompatibilityInformation,  
                           &ulEnableLFH, sizeof(ulEnableLFH)))  
        puts("Enabling Low Fragmentation Heap succeeded");  
    else  
        puts("Enabling Low Fragmentation Heap failed");  
    return 0;  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Выделение памяти](../../c-runtime-library/memory-allocation.md)