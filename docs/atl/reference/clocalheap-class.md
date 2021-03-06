---
description: 'Дополнительные сведения о: CLocalHeap Class'
title: Класс CLocalHeap
ms.date: 11/04/2016
f1_keywords:
- CLocalHeap
- ATLMEM/ATL::CLocalHeap
- ATLMEM/ATL::CLocalHeap::Allocate
- ATLMEM/ATL::CLocalHeap::Free
- ATLMEM/ATL::CLocalHeap::GetSize
- ATLMEM/ATL::CLocalHeap::Reallocate
helpviewer_keywords:
- CLocalHeap class
ms.assetid: 1ffa87a5-5fc8-4f8d-8809-58e87e963bd2
ms.openlocfilehash: 6cc168bc80182255017df3e3cdc970e5cfd56c7a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97141522"
---
# <a name="clocalheap-class"></a>Класс CLocalHeap

Этот класс реализует [иатлмеммгр](../../atl/reference/iatlmemmgr-class.md) с помощью функций локальной кучи Win32.

> [!IMPORTANT]
> Этот класс и его члены не могут использоваться в приложениях, выполняемых в среда выполнения Windows.

## <a name="syntax"></a>Синтаксис

```
class CLocalHeap : public IAtlMemMgr
```

## <a name="members"></a>Члены

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[CLocalHeap:: allocate](#allocate)|Вызовите этот метод, чтобы выделить блок памяти.|
|[CLocalHeap:: Free](#free)|Вызовите этот метод, чтобы освободить блок памяти, выделенный этим диспетчером памяти.|
|[CLocalHeap:: DataSize](#getsize)|Вызовите этот метод, чтобы получить выделенный размер блока памяти, выделенного этим диспетчером памяти.|
|[CLocalHeap:: перераспределение](#reallocate)|Вызовите этот метод для перераспределения памяти, выделенной данным диспетчером памяти.|

## <a name="remarks"></a>Комментарии

`CLocalHeap` реализует функции выделения памяти с помощью функций локальной кучи Win32.

> [!NOTE]
> Функции локальной кучи выполняются медленнее, чем другие функции управления памятью, и не предоставляют столько функций. Поэтому новые приложения должны использовать [функции кучи](/windows/win32/Memory/heap-functions). Они доступны в классе [CWin32Heap](../../atl/reference/cwin32heap-class.md) .

## <a name="example"></a>Пример

См. пример для [иатлмеммгр](../../atl/reference/iatlmemmgr-class.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`IAtlMemMgr`

`CLocalHeap`

## <a name="requirements"></a>Требования

**Заголовок:** атлмем. h

## <a name="clocalheapallocate"></a><a name="allocate"></a> CLocalHeap:: allocate

Вызовите этот метод, чтобы выделить блок памяти.

```
virtual __declspec(allocator) void* Allocate(size_t nBytes) throw();
```

### <a name="parameters"></a>Параметры

*nBytes*<br/>
Запрошенное число байтов в новом блоке памяти.

### <a name="return-value"></a>Возвращаемое значение

Возвращает указатель на начало выделенного блока памяти.

### <a name="remarks"></a>Комментарии

Вызовите метод [CLocalHeap:: Free](#free) или [CLocalHeap:: reallocate](#reallocate) , чтобы освободить память, выделенную этим методом.

Реализуется с помощью [локалаллок](/windows/win32/api/winbase/nf-winbase-localalloc) с параметром Flag LMEM_FIXED.

## <a name="clocalheapfree"></a><a name="free"></a> CLocalHeap:: Free

Вызовите этот метод, чтобы освободить блок памяти, выделенный этим диспетчером памяти.

```
virtual void Free(void* p) throw();
```

### <a name="parameters"></a>Параметры

*p*<br/>
Указатель на область памяти, выделенную ранее данным диспетчером памяти. Значение NULL является допустимым и не выполняет никаких действий.

### <a name="remarks"></a>Комментарии

Реализуется с помощью [функции LocalFree](/windows/win32/api/winbase/nf-winbase-localfree).

## <a name="clocalheapgetsize"></a><a name="getsize"></a> CLocalHeap:: DataSize

Вызовите этот метод, чтобы получить выделенный размер блока памяти, выделенного этим диспетчером памяти.

```
virtual size_t GetSize(void* p) throw();
```

### <a name="parameters"></a>Параметры

*p*<br/>
Указатель на область памяти, выделенную ранее данным диспетчером памяти.

### <a name="return-value"></a>Возвращаемое значение

Возвращает размер выделенного блока памяти в байтах.

### <a name="remarks"></a>Комментарии

Реализуется с помощью [локалсизе](/windows/win32/api/winbase/nf-winbase-localsize).

## <a name="clocalheapreallocate"></a><a name="reallocate"></a> CLocalHeap:: перераспределение

Вызовите этот метод для перераспределения памяти, выделенной данным диспетчером памяти.

```
virtual __declspec(allocator) void* Reallocate(void* p, size_t nBytes) throw();
```

### <a name="parameters"></a>Параметры

*p*<br/>
Указатель на область памяти, выделенную ранее данным диспетчером памяти.

*nBytes*<br/>
Запрошенное число байтов в новом блоке памяти.

### <a name="return-value"></a>Возвращаемое значение

Возвращает указатель на начало выделенного блока памяти.

### <a name="remarks"></a>Комментарии

Вызовите метод [CLocalHeap:: Free](#free) , чтобы освободить память, выделенную этим методом.

Реализуется с помощью [локалреаллок](/windows/win32/api/winbase/nf-winbase-localrealloc).

## <a name="see-also"></a>См. также раздел

[Общие сведения о классах](../../atl/atl-class-overview.md)<br/>
[Класс Ккомхеап](../../atl/reference/ccomheap-class.md)<br/>
[Класс CWin32Heap](../../atl/reference/cwin32heap-class.md)<br/>
[Класс CCRTHeap](../../atl/reference/cglobalheap-class.md)<br/>
[Класс Ккрсеап](../../atl/reference/ccrtheap-class.md)<br/>
[Класс Иатлмеммгр](../../atl/reference/iatlmemmgr-class.md)
