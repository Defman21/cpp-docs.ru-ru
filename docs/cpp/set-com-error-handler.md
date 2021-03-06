---
description: 'Дополнительные сведения: _set_com_error_handler'
title: _set_com_error_handler
ms.date: 11/04/2016
helpviewer_keywords:
- _set_com_error_handler function
ms.assetid: 49fe4fca-5e37-4d83-abaf-15be5ce37f94
ms.openlocfilehash: 88c59f30276089f28dc6e40b1ab5829bf68a7b4a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97116968"
---
# <a name="_set_com_error_handler"></a>_set_com_error_handler

Заменяет функцию по умолчанию, используемую для обработки ошибок COM. **_set_com_error_handler** зависит от корпорации Майкрософт.

## <a name="syntax"></a>Синтаксис

```cpp
void __stdcall _set_com_error_handler(
   void (__stdcall *pHandler)(
      HRESULT hr,
      IErrorInfo* perrinfo
   )
);
```

#### <a name="parameters"></a>Параметры

*фандлер*<br/>
Указатель на функцию замены.

*ч*<br/>
Сведения HRESULT.

*перринфо*<br/>
Объект `IErrorInfo`.

## <a name="remarks"></a>Комментарии

По умолчанию [_com_raise_error](../cpp/com-raise-error.md) обрабатывает все ошибки COM. Это поведение можно изменить с помощью **_set_com_error_handler** для вызова собственной функции обработки ошибок.

Функция замены должна иметь сигнатуру, эквивалентную сигнатуре `_com_raise_error`.

## <a name="example"></a>Пример

```cpp
// _set_com_error_handler.cpp
// compile with /EHsc
#include <stdio.h>
#include <comdef.h>
#include <comutil.h>

// Importing ado dll to attempt to establish an ado connection.
// Not related to _set_com_error_handler
#import "C:\Program Files\Common Files\System\ado\msado15.dll" no_namespace rename("EOF", "adoEOF")

void __stdcall _My_com_raise_error(HRESULT hr, IErrorInfo* perrinfo)
{
   throw "Unable to establish the connection!";
}

int main()
{
   _set_com_error_handler(_My_com_raise_error);
   _bstr_t bstrEmpty(L"");
   _ConnectionPtr Connection = NULL;
   try
   {
      Connection.CreateInstance(__uuidof(Connection));
      Connection->Open(bstrEmpty, bstrEmpty, bstrEmpty, 0);
   }
   catch(char* errorMessage)
   {
      printf("Exception raised: %s\n", errorMessage);
   }

   return 0;
}
```

```Output
Exception raised: Unable to establish the connection!
```

## <a name="requirements"></a>Требования

**Заголовок:**\<comdef.h>

**Библиотека:** Если указан параметр компилятора **/Zc: wchar_t** (по умолчанию), используйте комсуппв. lib или комсуппвд. lib. Если указан параметр **/Zc: wchar_t-** Compiler, используйте комсупп. lib. Дополнительные сведения, в том числе о том, как задать этот параметр в интегрированной среде разработки, см. в разделе [/Zc: wchar_t (wchar_t является собственным типом)](../build/reference/zc-wchar-t-wchar-t-is-native-type.md).

## <a name="see-also"></a>См. также раздел

[Глобальные функции компилятора COM](../cpp/compiler-com-global-functions.md)
