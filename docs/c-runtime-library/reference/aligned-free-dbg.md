---
description: 'Дополнительные сведения: _aligned_free_dbg'
title: _aligned_free_dbg
ms.date: 11/04/2016
api_name:
- _aligned_free_dbg
api_location:
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
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _aligned_free_dbg
- aligned_free_dbg
helpviewer_keywords:
- _aligned_free_dbg function
- aligned_free_dbg function
ms.assetid: eb0cb3c8-0992-4db8-bac3-65f1b8311ca6
ms.openlocfilehash: 7320cb800cf42f7b641ed1d60afaf5d2144990e8
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97335686"
---
# <a name="_aligned_free_dbg"></a>_aligned_free_dbg

Освобождает блок памяти, который был выделен с помощью [_aligned_malloc](aligned-malloc.md) или [_aligned_offset_malloc](aligned-offset-malloc.md) (только отладочная версия).

## <a name="syntax"></a>Синтаксис

```C
void _aligned_free_dbg(
   void *memblock
);
```

### <a name="parameters"></a>Параметры

*memblock*<br/>
Указатель на блок памяти, возвращенный функции [_aligned_malloc](aligned-malloc.md) или [_aligned_offset_malloc](aligned-offset-malloc.md) .

## <a name="remarks"></a>Комментарии

Функция **_aligned_free_dbg** является отладочной версией функции [_aligned_free](aligned-free.md) . Если [_DEBUG](../../c-runtime-library/debug.md) не определен, каждый вызов **_aligned_free_dbg** уменьшается до вызова `_aligned_free` . `_aligned_free`И, и **_aligned_free_dbg** освобождают блок памяти в базовой куче, но **_aligned_free_dbg** поддерживает функцию отладки: возможность сохранения освобожденных блоков в связанном списке кучи для имитации нехватки памяти.

**_aligned_free_dbg** выполняет проверку допустимости для всех указанных файлов и расположений блоков перед выполнением бесплатной операции. Приложение не ожидает предоставления этих сведений. Когда освобождается блок памяти, диспетчер отладочной кучи автоматически проверяет целостность буферов по обеим сторонам пользовательской части и выдает отчет об ошибке в случае их перезаписи. Если задано битовое поле _CRTDBG_DELAY_FREE_MEM_DF флага [_crtDbgFlag](../../c-runtime-library/crtdbgflag.md) , освобожденный блок заполняется значением 0xDD, ему назначается тип блока _FREE_BLOCK и хранится в связанном списке блоков памяти кучи.

В случае возникновения ошибки при освобождении памяти для `errno` задаются сведения о характере сбоя, полученные от операционной системы. Дополнительные сведения см. в разделе [errno, _doserrno, _sys_errlist и _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

Сведения о выделении, инициализации и управлении блоками памяти в отладочной версии базовой кучи, см. в статье [CRT Debug Heap Details](/visualstudio/debugger/crt-debug-heap-details). Сведения о типах блоков выделения и их использовании см. в разделе [типы блоков в отладочной куче](/visualstudio/debugger/crt-debug-heap-details). Сведения о различиях между вызовом стандартной функции кучи и ее отладочной версии в сборке отладки приложения см. в разделе [Версии отладки функций выделения кучи](/visualstudio/debugger/debug-versions-of-heap-allocation-functions).

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**_aligned_free_dbg**|\<crtdbg.h>|

Дополнительные сведения о совместимости см. в разделе [Compatibility](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>См. также раздел

[Отладочные подпрограммы](../../c-runtime-library/debug-routines.md)
