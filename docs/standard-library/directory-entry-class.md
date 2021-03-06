---
description: 'Дополнительные сведения о: directory_entry классе'
title: Класс directory_entry
ms.date: 09/10/2018
f1_keywords:
- filesystem/std::experimental::filesystem::directory_entry
- filesystem/std::experimental::filesystem::directory_entry::operator const std::experimental::filesystem::path &
- filesystem/std::experimental::filesystem::directory_entry::directory_entry
- filesystem/std::experimental::filesystem::directory_entry::operator=
- filesystem/std::experimental::filesystem::directory_entry::assign
- filesystem/std::experimental::filesystem::directory_entry::replace_filename
- filesystem/std::experimental::filesystem::directory_entry::path
- filesystem/std::experimental::filesystem::directory_entry::status
- filesystem/std::experimental::filesystem::directory_entry::symlink_status
- filesystem/std::experimental::filesystem::directory_entry::operator&lt;
- filesystem/std::experimental::filesystem::directory_entry::operator==
- filesystem/std::experimental::filesystem::directory_entry::operator!=
- filesystem/std::experimental::filesystem::directory_entry::operator&lt;=
- filesystem/std::experimental::filesystem::directory_entry::operator&gt;
- filesystem/std::experimental::filesystem::directory_entry::operator&gt;=
ms.assetid: 1827c67b-4137-4548-adb0-f955f7acaf08
helpviewer_keywords:
- std::experimental::filesystem::directory_entry
- std::experimental::filesystem::directory_entry::operator const std::experimental::filesystem::path &
- std::experimental::filesystem::directory_entry::directory_entry
- std::experimental::filesystem::directory_entry::operator=
- std::experimental::filesystem::directory_entry::assign
- std::experimental::filesystem::directory_entry::replace_filename
- std::experimental::filesystem::directory_entry::path
- std::experimental::filesystem::directory_entry::status
- std::experimental::filesystem::directory_entry::symlink_status
- std::experimental::filesystem::directory_entry::operator&lt;
- std::experimental::filesystem::directory_entry::operator==
- std::experimental::filesystem::directory_entry::operator!=
- std::experimental::filesystem::directory_entry::operator&lt;=
- std::experimental::filesystem::directory_entry::operator&gt;
- std::experimental::filesystem::directory_entry::operator&gt;=
ms.openlocfilehash: a4a4b69e9f568c19eefae79554838fac5781f3f8
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97324552"
---
# <a name="directory_entry-class"></a>Класс directory_entry

Описывает объект, возвращаемый `*X`, где *X* — [directory_iterator](../standard-library/directory-iterator-class.md) или [recursive_directory_iterator](../standard-library/recursive-directory-iterator-class.md).

## <a name="syntax"></a>Синтаксис

```cpp
class directory_entry;
```

## <a name="remarks"></a>Remarks

Класс сохраняет объект типа [path](../standard-library/path-class.md). Сохраненный `path` может быть экземпляром [класса path](../standard-library/path-class.md) или типом, производным от `path`. Он также сохраняет два значения [file_type](../standard-library/filesystem-enumerations.md#file_type); одно из них представляет то, что известно о состоянии сохраненного имени файла, а другое представляет то, что известно о состоянии символьной ссылки имени файла.

Дополнительные сведения и примеры кода см. в разделе [Навигация по файловой системе (C++)](../standard-library/file-system-navigation.md).

### <a name="constructors"></a>Конструкторы

|Конструктор|Описание|
|-|-|
|[directory_entry](#directory_entry)|Установленные по умолчанию конструкторы работают корректно. Четвертый конструктор инициализируется `mypath` как *Pval*, `mystat` для *stat_arg* и `mysymstat` для *symstat_arg*.|

### <a name="member-functions"></a>Функции элементов

|Функция-член|Описание|
|-|-|
|[assign](#assign)|Функция члена присваивает значения *Pval* `mypath` , *stat* to `mystat` и *симстат* `mysymstat` .|
|[путь](#path)|Функция-член возвращает значение `mypath`.|
|[replace_filename](#replace_filename)|Функция члена заменяется `mypath` на `mypath.parent_path()`  /  *Pval*, `mystat` с *stat_arg* и `mysymstat` с *symstat_arg*|
|[status](#status)|Обе функции члена возвращают `mystat` , возможно, первое изменение.|
|[symlink_status](#symlink_status)|Обе функции члена возвращают `mysymstat` , возможно, первое изменение.|

### <a name="operators"></a>Операторы

|Оператор|Описание|
|-|-|
|[operator! =](#op_neq)|Заменяет элементы списка копией другого списка.|
|[Оператор =](#op_as)|Операторы-члены присваивания по умолчанию работают корректно.|
|[Оператор = =](#op_eq)|Возвращает `mypath == right.mypath`.|
|[Оператор<](#op_lt)|Возвращает `mypath < right.mypath`.|
|[Оператор<=](#op_lteq)|Возвращает `!(right < *this)`.|
|[Оператор>](#op_gt)|Возвращает `right < *this`.|
|[Оператор>=](#op_gteq)|Возвращает `!(*this < right)`.|
|[Константа оператора const path_type&](#path_type)|Возвращает `mypath`.|

## <a name="requirements"></a>Требования

**Заголовок:** \< экспериментальная или файловая система&gt;

**Пространство имен:** std::experimental::filesystem

## <a name="assign"></a><a name="assign"></a> назначать

Функция члена присваивает *Pval* `mypath` , *stat_arg* `mystat` , и *symstat_arg* в `mysymstat` .

```cpp
void assign(const std::experimental::filesystem::path& pval,
    file_status stat_arg = file_status(),
    file_status symstat_arg = file_status());
```

### <a name="parameters"></a>Параметры

*Pval*\
Путь к сохраненному имени файла.

*stat_arg*\
Состояние сохраненного имени файла.

*symstat_arg*\
Состояние символьной ссылки для имени сохраненного файла.

## <a name="directory_entry"></a><a name="directory_entry"></a> directory_entry

Установленные по умолчанию конструкторы работают корректно. Четвертый конструктор инициализируется `mypath` как *Pval*, `mystat` для *stat_arg* и `mysymstat` для *symstat_arg*.

```cpp
directory_entry() = default;
directory_entry(const directory_entry&) = default;
directory_entry(directory_entry&&) noexcept = default;
explicit directory_entry(const std::experimental::filesystem::path& pval,
    file_status stat_arg = file_status(),
    file_status symstat_arg = file_status());
```

### <a name="parameters"></a>Параметры

*Pval*\
Путь к сохраненному имени файла.

*stat_arg*\
Состояние сохраненного имени файла.

*symstat_arg*\
Состояние символьной ссылки для имени сохраненного файла.

## <a name="operator"></a><a name="op_neq"></a> operator! =

Функция-член возвращает значение `!(*this == right)`.

```cpp
bool operator!=(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operator"></a><a name="op_as"></a> Оператор =

Операторы-члены присваивания по умолчанию работают корректно.

```cpp
directory_entry& operator=(const directory_entry&) = default;
directory_entry& operator=(directory_entry&&) noexcept = default;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) , копируемый в `directory_entry` .

## <a name="operator"></a><a name="op_eq"></a> Оператор = =

Функция-член возвращает значение `mypath == right.mypath`.

```cpp
bool operator==(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operatorlt"></a><a name="op_lt"></a> станции&lt;

Функция-член возвращает значение `mypath < right.mypath`.

```cpp
bool operator<(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operatorlt"></a><a name="op_lteq"></a> станции&lt;=

Функция-член возвращает значение `!(right < *this)`.

```cpp
bool operator&lt;=(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operatorgt"></a><a name="op_gt"></a> станции&gt;

Функция-член возвращает значение `right < *this`.

```cpp
bool operator&gt;(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operatorgt"></a><a name="op_gteq"></a> станции&gt;=

Функция-член возвращает значение `!(*this < right)`.

```cpp
bool operator&gt;=(const directory_entry& right) const noexcept;
```

### <a name="parameters"></a>Параметры

*Правильно*\
[Directory_entry](../standard-library/directory-entry-class.md) сравнивается с `directory_entry` .

## <a name="operator-const-path_type"></a><a name="path_type"></a> Константа оператора const path_type&

Оператор-член возвращает `mypath`.

```cpp
operator const std::experimental::filesystem::path&() const;
```

## <a name="path"></a><a name="path"></a> путь

Функция-член возвращает значение `mypath`.

```cpp
const std::experimental::filesystem::path& path() const noexcept;
```

## <a name="replace_filename"></a><a name="replace_filename"></a> replace_filename

Функция члена заменяется `mypath` на `mypath.parent_path()`  /  *Pval*, `mystat` с *stat_arg* и `mysymstat` с *symstat_arg*

```cpp
void replace_filename(
    const std::experimental::filesystem::path& pval,
    file_status stat_arg = file_status(),
    file_status symstat_arg = file_status());
```

### <a name="parameters"></a>Параметры

*Pval*\
Путь к сохраненному имени файла.

*stat_arg*\
Состояние сохраненного имени файла.

*symstat_arg*\
Состояние символьной ссылки для имени сохраненного файла.

## <a name="status"></a><a name="status"></a> состояние

Обе функции члена возвращают `mystat` , возможно, первое изменение следующим образом:

1. Если `status_known(mystat)` не выполнять никаких действий.

1. В противном случае — значение `!status_known(mysymstat) && !is_symlink(mysymstat)` `mystat = mysymstat` .

```cpp
file_status status() const;
file_status status(error_code& ec) const noexcept;
```

### <a name="parameters"></a>Параметры

*контроллер*\
Код ошибки состояния.

## <a name="symlink_status"></a><a name="symlink_status"></a> symlink_status

Обе функции члена возвращают `mysymstat` , возможно, первое изменение следующим образом: Если `status_known(mysymstat)` не выполнять никаких действий. В противном случае — значение `mysymstat = symlink_status(mypval)`.

```cpp
file_status symlink_status() const;
file_status symlink_status(error_code& ec) const noexcept;
```

### <a name="parameters"></a>Параметры

*контроллер*\
Код ошибки состояния.

## <a name="see-also"></a>См. также раздел

[Справочник по файлам заголовков](../standard-library/cpp-standard-library-header-files.md)\
[\<системой&gt;](../standard-library/filesystem.md)
