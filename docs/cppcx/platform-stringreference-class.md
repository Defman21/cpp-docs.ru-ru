---
description: 'Дополнительные сведения о классе Platform:: StringReference'
title: Класс Platform::StringReference
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- VCCORLIB/Platform::StringReference::StringReference
- VCCORLIB/Platform::StringReference::Data
- VCCORLIB/Platform::StringReference::Length
- VCCORLIB/Platform::StringReference::GetHSTRING
- VCCORLIB/Platform::StringReference::GetString
ms.assetid: 2d09c7ec-0f16-458e-83ed-7225a1b9221e
ms.openlocfilehash: 5c211776bccbd3ba2fedaf769502f7dad71b6eb6
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97307955"
---
# <a name="platformstringreference-class"></a>Класс Platform::StringReference

Тип оптимизации, который можно использовать для передачи строковых данных из входных параметров `Platform::String^` в другие методы с минимальным числом операций копирования.

## <a name="syntax"></a>Синтаксис

```cpp
class StringReference
```

### <a name="remarks"></a>Remarks

### <a name="members"></a>Элементы

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[StringReference:: StringReference](#ctor)|Два конструктора для создания экземпляров `StringReference`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[StringReference::D ATA](#data)|Возвращает строковые данные как массив значений char16.|
|[StringReference:: Length](#length)|Возвращает число символов в строке.|
|[StringReference:: Жесстринг](#gethstring)|Возвращает строковые данные как HSTRING.|
|[StringReference:: GetString](#getstring)|Возвращает строковые данные как `Platform::String^`.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Описание|
|----------|-----------------|
|[StringReference:: operator =](#operator-assign)|Присваивает `StringReference` новому экземпляру `StringReference` .|
|[StringReference:: operator ()](#operator-call)|Преобразует `StringReference` в `Platform::String^`.|

### <a name="requirements"></a>Требования

**Минимальный поддерживаемый клиент:** Windows 8

**Минимальный поддерживаемый сервер:** Windows Server 2012

**Пространство имен:** Platform

**Заголовок:** vccorlib.h

## <a name="stringreferencedata-method"></a><a name="data"></a> StringReference::D метод ATA

Возвращает содержимое этой строки `StringReference` как массив значений char16.

### <a name="syntax"></a>Синтаксис

```cpp
const ::default::char16 * Data() const;
```

### <a name="return-value"></a>Возвращаемое значение

Массив текстовых символов ЮНИКОДА char16.

## <a name="stringreferencegethstring-method"></a><a name="gethstring"></a> Метод StringReference:: Жесстринг

Возвращает содержимое строки как `__abi_HSTRING`.

### <a name="syntax"></a>Синтаксис

```cpp
__abi_HSTRING GetHSTRING() const;
```

### <a name="return-value"></a>Возвращаемое значение

Объект `__abi_HSTRING`, который содержит строковые данные.

### <a name="remarks"></a>Комментарии

## <a name="stringreferencegetstring-method"></a><a name="getstring"></a> Метод StringReference:: GetString

Возвращает содержимое строки как `Platform::String^`.

### <a name="syntax"></a>Синтаксис

```cpp
__declspec(no_release_return) __declspec(no_refcount)
    ::Platform::String^ GetString() const;
```

### <a name="return-value"></a>Возвращаемое значение

Объект `Platform::String^`, который содержит строковые данные.

## <a name="stringreferencelength-method"></a><a name="length"></a> Метод StringReference:: Length

Возвращает число символов в строке.

### <a name="syntax"></a>Синтаксис

```cpp
unsigned int Length() const;
```

### <a name="return-value"></a>Возвращаемое значение

Целое число без знака, указывающее число символов в строке.

### <a name="remarks"></a>Комментарии

## <a name="stringreferenceoperator-operator"></a><a name="operator-assign"></a> Оператор StringReference:: operator =

Присваивает указанный объект текущему объекту `StringReference`.

### <a name="syntax"></a>Синтаксис

```cpp
StringReference& operator=(const StringReference& __fstrArg);
StringReference& operator=(const ::default::char16* __strArg);
```

### <a name="parameters"></a>Параметры

*__fstrArg*<br/>
Адрес объекта `StringReference`, используемый для инициализации текущего объекта `StringReference`.

*__strArg*<br/>
Указатель на массив значений char16, используемый для инициализации текущего объекта `StringReference`.

### <a name="return-value"></a>Возвращаемое значение

Ссылка на объект типа `StringReference`.

### <a name="remarks"></a>Комментарии

Поскольку `StringReference` является стандартным классом C++, а не классом ссылки, он не отображается в **обозревателе объектов**.

## <a name="stringreferenceoperator--operator"></a><a name="operator-call"></a> Оператор StringReference:: operator ()

Преобразует объект `StringReference` в объект `Platform::String^`.

### <a name="syntax"></a>Синтаксис

```cpp
__declspec(no_release_return) __declspec(no_refcount)
         operator ::Platform::String^() const;
```

### <a name="return-value"></a>Возвращаемое значение

Дескриптор для объекта типа `Platform::String`.

## <a name="stringreferencestringreference-constructor"></a><a name="ctor"></a> Конструктор StringReference:: StringReference

Инициализирует новый экземпляр класса `StringReference`.

### <a name="syntax"></a>Синтаксис

```cpp
StringReference();
StringReference(const StringReference& __fstrArg);
StringReference(const ::default::char16* __strArg);
StringReference(const ::default::char16* __strArg, size_t __lenArg);
```

### <a name="parameters"></a>Параметры

*__fstrArg*<br/>
Объект `StringReference`, данные которого используются для инициализации нового экземпляра.

*__strArg*<br/>
Указатель на массив значений char16, используемый для инициализации нового экземпляра.

*__lenArg*<br/>
Число элементов в `__strArg`.

### <a name="remarks"></a>Комментарии

Первая версия этого конструктора является конструктором по умолчанию. Вторая версия инициализирует новый экземпляра класса `StringReference` из объекта, заданного параметром `__fstrArg`. Третья и четвертая перегрузки инициализируют новый экземпляр класса `StringReference` из массива значений char16. char16 представляет 16-разрядный текстовый символ ЮНИКОДА.

## <a name="see-also"></a>См. также раздел

[Класс Platform:: StringReference](../cppcx/platform-stringreference-class.md)
