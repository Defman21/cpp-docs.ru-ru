---
title: "_com_raise_error | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- _com_raise_error
dev_langs:
- C++
helpviewer_keywords:
- _com_raise_error function
ms.assetid: a98226c2-c3fe-44f1-8ff5-85863de11cd6
caps.latest.revision: 10
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: 1f2072a6f3a6f78bc6751e39e0c79d978845fe97
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="comraiseerror"></a>_com_raise_error
**Блок, относящийся только к системам Майкрософт**  
  
 Создает [_com_error](../cpp/com-error-class.md) в ответ на ошибку.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
      void __stdcall _com_raise_error(  
   HRESULT hr,  
   IErrorInfo* perrinfo = 0  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `hr`  
 Информация о значении `HRESULT`.  
  
 `perrinfo`  
 **IErrorInfo** объекта.  
  
## <a name="remarks"></a>Примечания  
 Параметр `_com_raise_error`, заданный в comdef.h, можно заменить пользовательской версией с тем же именем и прототипом. Это можно сделать, если требуется использовать `#import` без обработки исключений C++. В этом случае пользователь версии **_com_raise_error** может потребоваться сделать `longjmp` или окно с сообщением и остановки процесса. Однако пользовательская версия не должна возвращаться, поскольку код поддержки COM в компиляторе не ожидает ее возврата.  
  
 Можно также использовать [_set_com_error_handler](../cpp/set-com-error-handler.md) для замены функции обработки ошибок по умолчанию.  
  
 По умолчанию `_com_raise_error` определяется следующим образом.  
  
```  
void __stdcall _com_raise_error(HRESULT hr, IErrorInfo* perrinfo) {  
   throw _com_error(hr, perrinfo);  
}  
```  
  
**Завершение блока, относящегося только к системам Майкрософт**  
  
## <a name="requirements"></a>Требования  
 **Заголовок:** comdef.h  
  
 **LIB:** Если **wchar_t — собственный тип** включен параметр компилятора, используйте comsuppw.lib или comsuppwd.lib. Если **wchar_t — собственный тип** параметр отключен, используйте comsupp.lib. Дополнительные сведения см. в разделе [/Zc:wchar_t (wchar_t — это собственный тип)](../build/reference/zc-wchar-t-wchar-t-is-native-type.md).  
  
## <a name="see-also"></a>См. также  
 [Глобальные функции COM компилятора](../cpp/compiler-com-global-functions.md)   
 [_set_com_error_handler](../cpp/set-com-error-handler.md)