---
description: 'Дополнительные сведения: создание исключений программного обеспечения'
title: Создание исключений программного обеспечения
ms.date: 11/04/2016
helpviewer_keywords:
- run-time errors, treating as exceptions
- exception handling [C++], errors as exceptions
- exceptions [C++], flagging errors as exceptions
- errors [C++], treating as exceptions
- exception handling [C++], detecting errors
- structured exception handling [C++], errors as exceptions
- exceptions [C++], software
- RaiseException function
- software exceptions [C++]
- formats [C++], exception codes
ms.assetid: be1376c3-c46a-4f52-ad1d-c2362840746a
ms.openlocfilehash: 737bec4af99ad7743a8f7740d57919f169c2b509
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97319408"
---
# <a name="raising-software-exceptions"></a>Создание исключений программного обеспечения

Некоторые из самых распространенных источников ошибок программы не отмечены системой как исключения. Например, при попытке выделить блок памяти при недостаточной памяти среда выполнения или функция API не создает исключение, но возвращает код ошибки.

Тем не менее можно рассматривать любое условие как исключение, выявляя это условие в коде, а затем сообщая о нем, вызвав функцию [RaiseException](/windows/win32/api/errhandlingapi/nf-errhandlingapi-raiseexception) . Отмечая ошибки таким образом, можно использовать преимущества структурированной обработки исключений в любом типе ошибки времени выполнения.

Чтобы использовать структурированную обработку исключений с ошибками, выполните следующие действия.

- Определите собственный код исключения для события.

- Вызов `RaiseException` при обнаружении проблемы.

- Используйте фильтры обработки исключений для проверки определенного кода исключения.

В \<winerror.h> файле отображается формат кодов исключений. Чтобы проверить, что определяемый код не будет конфликтовать с существующим кодом исключения, задайте для третьего наиболее значимого бита значение 1. Следует установить четыре наиболее значимых бита, как показано в следующей таблице.

|Bits|Рекомендуемый двоичный параметр|Описание|
|----------|--------------------------------|-----------------|
|31-30|11|Эти два бита описываются основное состояние кода: 11 = ошибка, 00 = успех, 01 = информация, 10 = предупреждение.|
|29|1|Бит клиента. Установите значение 1 для пользовательских кодов.|
|28|0|Зарезервированный бит. (Оставьте значение 0.)|

При желании для первых двух битов можно задать параметр, отличный от двоичного параметра 11, хотя параметр "ошибка" подходит для большинства исключений. Помните, что биты 29 и 28 следует установить так, как показано в предыдущей таблице.

В результате код ошибки должен иметь старшие четыре бита, равные шестнадцатеричному E. Например, следующие определения определяют коды исключений, которые не конфликтуют с кодами исключений Windows. (Хотя может потребоваться проверить, какие коды используются сторонними библиотеками DLL.)

```cpp
#define STATUS_INSUFFICIENT_MEM       0xE0000001
#define STATUS_FILE_BAD_FORMAT        0xE0000002
```

После определения кода исключения его можно использовать для создания исключения. Например, следующий код вызывает `STATUS_INSUFFICIENT_MEM` исключение в ответ на проблему выделения памяти:

```cpp
lpstr = _malloc( nBufferSize );
if (lpstr == NULL)
    RaiseException( STATUS_INSUFFICIENT_MEM, 0, 0, 0);
```

Если требуется просто создать исключение, можно установить для трех последних параметров значение 0. Три последних параметра полезны при передаче дополнительной информации и установке флага, который запрещает обработчикам продолжать выполнение. Дополнительные сведения см. в описании функции [RaiseException](/windows/win32/api/errhandlingapi/nf-errhandlingapi-raiseexception) в Windows SDK.

Затем можно проверить определенные коды в фильтрах обработки исключений. Пример:

```cpp
__try {
    ...
}
__except (GetExceptionCode() == STATUS_INSUFFICIENT_MEM ||
        GetExceptionCode() == STATUS_FILE_BAD_FORMAT )
```

## <a name="see-also"></a>См. также раздел

[Написание обработчика исключений](../cpp/writing-an-exception-handler.md)<br/>
[Структурированная обработка исключений (C/C++)](../cpp/structured-exception-handling-c-cpp.md)
