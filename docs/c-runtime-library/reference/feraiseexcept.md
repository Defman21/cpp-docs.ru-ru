---
description: 'Дополнительные сведения о: фераисиксцепт'
title: feraiseexcept
ms.date: 04/05/2018
api_name:
- feraiseexcept
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
- HeaderDef
f1_keywords:
- feraiseexcept
- fenv/feraiseexcept
helpviewer_keywords:
- feraiseexcept function
ms.assetid: 87e89151-83c2-4563-9a9a-45666245d437
ms.openlocfilehash: 8e7a06006cfdc768fdaa306bc293857f1c375b90
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97124947"
---
# <a name="feraiseexcept"></a>feraiseexcept

Вызывает указанные исключения с плавающей запятой.

## <a name="syntax"></a>Синтаксис

```C
int feraiseexcept(
   int excepts
);
```

### <a name="parameters"></a>Параметры

*Кроме*<br/>
Исключения с плавающей запятой, которые необходимо вызвать.

## <a name="return-value"></a>Возвращаемое значение

Если все заданные исключения вызваны успешно, возвращается 0.

## <a name="remarks"></a>Комментарии

Функция **фераисиксцепт** пытается вызвать исключения с плавающей запятой, заданные параметром *except*.   Функция **фераисиксцепт** поддерживает эти макросы исключений, определенные в \<fenv.h> :

|Макрос исключения|Описание|
|---------------------|-----------------|
|FE_DIVBYZERO|При выполнении предыдущей операции с плавающей запятой произошла ошибка сингулярности или полюса, в результате чего было получено бесконечное значение.|
|FE_INEXACT|Функция принудительно округлила сохраненный результат ранее выполненной операции с плавающей запятой.|
|FE_INVALID|Ошибка домена в ранее выполненной операции с плавающей запятой.|
|FE_OVERFLOW|Ошибка диапазона. Ранее выполненная операция с плавающей запятой возвратила слишком большое значение, которое не удается представить.|
|FE_UNDERFLOW|Ранее выполненная операция с плавающей запятой возвратила слишком малое значение, которое не удается представить с полной точностью. Создано денормализованное значение.|
|FE_ALL_EXCEPT|Побитовая операция ИЛИ для всех поддерживаемых исключений с плавающей запятой.|

Аргумент *except* может иметь значение 0, одно из значений макросов исключений или побитовое или двух или более поддерживаемых макросов исключений. Если один из указанных макросов исключений имеет значение FE_OVERFLOW или FE_UNDERFLOW, в качестве побочного эффекта может быть вызвано исключение FE_INEXACT.

Чтобы использовать эту функцию, необходимо отключить оптимизацию вычислений с плавающей запятой, которая может препятствовать доступу. Для этого следует использовать директиву `#pragma fenv_access(on)` перед вызовом. Дополнительные сведения см. в разделе [fenv_access](../../preprocessor/fenv-access.md).

**Зависит от корпорации Майкрософт:** Исключения, указанные в *except* , вызываются в порядке FE_INVALID, FE_DIVBYZERO, FE_OVERFLOW, FE_UNDERFLOW, FE_INEXACT. Однако FE_INEXACT могут возникать при возникновении FE_OVERFLOW или FE_UNDERFLOW, даже если они не указаны в *except*.

## <a name="requirements"></a>Требования

|Функция|Заголовок C|Заголовок C++|
|--------------|--------------|------------------|
|*feraiseexcept*|\<fenv.h>|\<cfenv>|

Дополнительные сведения о совместимости см. в статье [Compatibility](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>См. также раздел

[Алфавитный справочник по функциям](crt-alphabetical-function-reference.md)<br/>
[fesetexceptflag](fesetexceptflag2.md)<br/>
[feholdexcept](feholdexcept2.md)<br/>
[fetestexcept](fetestexcept1.md)<br/>
[feupdateenv](feupdateenv.md)<br/>
