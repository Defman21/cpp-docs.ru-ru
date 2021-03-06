---
description: Дополнительные сведения о функциях пространства имен Concurrency (AMP)
title: Функции пространства имен Concurrency (AMP)
ms.date: 11/04/2016
f1_keywords:
- amp/Concurrency::all_memory_fence
- amp/Concurrency::atomic_compare_exchange
- amp/Concurrency::atomic_fetch_dec
- amp/Concurrency::atomic_fetch_max
- amp/Concurrency::atomic_fetch_min
- amp/Concurrency::copy
- amp/Concurrency::direct3d_abort
- amp/Concurrency::direct3d_printf
- amp/Concurrency::global_memory_fence
- amp/Concurrency::tile_static_memory_fence
ms.assetid: 2bef0985-cb90-4ece-90b9-66529aec73c9
ms.openlocfilehash: 65255f14acdc402003be46de5f978da6d9a8f8ff
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97211821"
---
# <a name="concurrency-namespace-functions-amp"></a>Функции пространства имен Concurrency (AMP)

:::row:::
   :::column span="":::
      [`all_memory_fence`](#all_memory_fence)\
      [`amp_uninitialize`](#amp_uninitialize)\
      [`atomic_compare_exchange`](#atomic_compare_exchange)\
      [`atomic_exchange`](#atomic_exchange)\
      [`atomic_fetch_add`](#atomic_fetch_add)\
      [`atomic_fetch_and`](#atomic_fetch_and)
   :::column-end:::
   :::column span="":::
      [`atomic_fetch_dec`](#atomic_fetch_dec)\
      [`atomic_fetch_inc`](#atomic_fetch_inc)\
      [`atomic_fetch_max`](#atomic_fetch_max)\
      [`atomic_fetch_min`](#atomic_fetch_min)\
      [`atomic_fetch_or`](#atomic_fetch_or)
   :::column-end:::
   :::column span="":::
      [`atomic_fetch_sub`](#atomic_fetch_sub)\
      [`atomic_fetch_xor`](#atomic_fetch_xor)\
      [`copy`](#copy)\
      [`copy_async`](#copy_async)\
      [`direct3d_abort`](#direct3d_abort)
   :::column-end:::
   :::column span="":::
      [`direct3d_errorf`](#direct3d_errorf)\
      [`direct3d_printf`](#direct3d_printf)\
      [`global_memory_fence`](#global_memory_fence)\
      [`parallel_for_each`](#parallel_for_each)\
      [`tile_static_memory_fence`](#tile_static_memory_fence)
   :::column-end:::
:::row-end:::

## <a name="all_memory_fence"></a><a name="all_memory_fence"></a> all_memory_fence

Блокирует выполнение всех потоков в плитке до тех пор, пока не будут завершены все обращения к памяти. Это гарантирует, что все обращения к памяти видимы для других потоков в плитке потока и выполняются в порядке программ.

```cpp
inline void all_memory_fence(const tile_barrier& _Barrier) restrict(amp);
```

### <a name="parameters"></a>Параметры

*_Barrier*<br/>
Объект `tile_barrier`.

## <a name="amp_uninitialize"></a><a name="amp_uninitialize"></a> amp_uninitialize

Отменяет инициализацию среды выполнения C++ AMP. Допустимо вызывать эту функцию несколько раз во время существования приложения. Вызов API C++ AMP после вызова этой функции приведет к повторной инициализации среды выполнения C++ AMP. Обратите внимание, что использование C++ AMP объектов в вызовах этой функции недопустимо, и это приводит к неопределенному поведению. Кроме того, параллельное вызов этой функции и других интерфейсов API AMP является недопустимым и приведет к неопределенному поведению.

```cpp
void __cdecl amp_uninitialize();
```

## <a name="atomic_compare_exchange"></a><a name="atomic_compare_exchange"></a> atomic_compare_exchange

Атомарно сравнивает значение, хранящееся в месте в памяти, указанном в первом аргументе, на равенство со значением второго указанного аргумента, и если значения совпадают, то значение в расположении в памяти изменяется на то, что соответствует третьему указанному аргументу.

```cpp
inline bool atomic_compare_exchange(
    _Inout_ int* _Dest,
    _Inout_ int* _Expected_value,
    int value
    ) restrict(amp)

inline bool atomic_compare_exchange(
    _Inout_ unsigned int* _Dest,
    _Inout_ unsigned int* _Expected_value,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Расположение, из которого считывается одно из сравниваемых значений, и для которого должно быть сохранено новое значение (при его наличии).

*_Expected_value*<br/>
Расположение, из которого считывается второе сравниваемое значение.

*value*<br/>
Значение, которое должно храниться в памяти, указанной в параметре, `_Dest` Если равен `_Dest` `_Expected_value` .

### <a name="return-value"></a>Возвращаемое значение

**`true`** значение, если операция выполнена успешно; в противном случае — **`false`** .

## <a name="atomic_exchange-function-c-amp"></a><a name="atomic_exchange"></a> Функция atomic_exchange (C++ AMP)

Задает значение целевого расположения в качестве атомарной операции.

```cpp
inline int atomic_exchange(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_exchange(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)

inline float atomic_exchange(
    _Inout_ float* _Dest,
    float value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на целевое расположение.

*value*<br/>
Новое значение.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение целевого расположения.

## <a name="atomic_fetch_add-function-c-amp"></a><a name="atomic_fetch_add"></a> Функция atomic_fetch_add (C++ AMP)

Атомарным образом добавьте значение в значение расположения в памяти.

```cpp
inline int atomic_fetch_add(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_add(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на расположение в памяти.

*value*<br/>
Добавляемое значение.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение расположения в памяти.

## <a name="atomic_fetch_and-function-c-amp"></a><a name="atomic_fetch_and"></a> Функция atomic_fetch_and (C++ AMP)

Атомарно выполняет побитовую операцию и для значения и значение расположения в памяти.

```cpp
inline int atomic_fetch_and(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_and(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на расположение в памяти.

*value*<br/>
Значение, используемое в битовом вычислении и.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение расположения в памяти.

## <a name="atomic_fetch_dec"></a><a name="atomic_fetch_dec"></a> atomic_fetch_dec

Атомарно уменьшает значение, хранящееся в указанном расположении в памяти.

```cpp
inline int atomic_fetch_dec(_Inout_ int* _Dest
    ) restrict(amp)

inline unsigned int atomic_fetch_dec(_Inout_ unsigned int* _Dest) restrict(amp);
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Место в памяти для значения, которое необходимо уменьшить.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение, хранящееся в расположении в памяти.

## <a name="atomic_fetch_inc"></a><a name="atomic_fetch_inc"></a> atomic_fetch_inc

Атомарно увеличивает значение, хранящееся в указанном расположении в памяти.

```cpp
inline int atomic_fetch_inc(_Inout_ int* _Dest) restrict(amp);

inline unsigned int atomic_fetch_inc(_Inout_ unsigned int* _Dest) restrict(amp);
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Расположение в памяти значения, которое должно быть увеличено.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение, хранящееся в расположении в памяти.

## <a name="atomic_fetch_max"></a><a name="atomic_fetch_max"></a> atomic_fetch_max

Атомарно выполняет вычисление максимального значения между значением, хранящимся в памяти, заданным в первом аргументе, и значением, указанным во втором аргументе, и сохраняет его в одном и том же месте в памяти.

```cpp
inline int atomic_fetch_max(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_max(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Расположение, из которого считывается одно из сравниваемых значений, и в котором должно храниться максимальное из двух значений.

*value*<br/>
Значение, сравниваемое со значением в указанном расположении.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение, хранящееся в указанном расположении.

## <a name="atomic_fetch_min"></a><a name="atomic_fetch_min"></a> atomic_fetch_min

Атомарно выполняет вычисление минимального значения между значением, хранящимся в памяти, заданным в первом аргументе, и значением, указанным во втором аргументе, и сохраняет его в том же расположении в памяти.

```cpp
inline int atomic_fetch_min(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_min(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Расположение, из которого считывается одно из сравниваемых значений, и в которое необходимо сохранить минимальное из двух значений.

*value*<br/>
Значение, сравниваемое со значением в указанном расположении.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение, хранящееся в указанном расположении.

## <a name="atomic_fetch_or-function-c-amp"></a><a name="atomic_fetch_or"></a> Функция atomic_fetch_or (C++ AMP)

Атомарно выполняет операцию побитового или со значением и значением расположения в памяти.

```cpp
inline int atomic_fetch_or(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_or(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на расположение в памяти.

*value*<br/>
Значение, используемое в битовом вычислении или.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение расположения в памяти.

## <a name="atomic_fetch_sub-function-c-amp"></a><a name="atomic_fetch_sub"></a> Функция atomic_fetch_sub (C++ AMP)

Атомарным образом вычитает значение из места в памяти.

```cpp
inline int atomic_fetch_sub(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_sub(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на целевое расположение.

*value*<br/>
Значение для вычитания.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение расположения в памяти.

## <a name="atomic_fetch_xor-function-c-amp"></a><a name="atomic_fetch_xor"></a> Функция atomic_fetch_xor (C++ AMP)

Атомарно выполняет побитовую операцию XOR со значением и местом в памяти.

```cpp
inline int atomic_fetch_xor(
    _Inout_ int* _Dest,
    int value
    ) restrict(amp)

inline unsigned int atomic_fetch_xor(
    _Inout_ unsigned int* _Dest,
    unsigned int value
    ) restrict(amp)
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Указатель на расположение в памяти.

*value*<br/>
Значение, используемое в вычислении XOR.

### <a name="return-value"></a>Возвращаемое значение

Исходное значение расположения в памяти.

## <a name="copy"></a><a name="copy"></a> копии

Копирует объект C++ AMP. Выполнены все синхронные требования к переносу данных. Нельзя копировать данные при выполнении кода в ускорителе. Общая форма этой функции — `copy(src, dest)` .

```cpp
template <typename value_type, int _Rank>
void copy(
    const array<value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
void copy(
    InputIterator _SrcFirst,
    InputIterator _SrcLast,
    array<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
void copy(
    InputIterator _SrcFirst,
    array<value_type, _Rank>& _Dest);

template <typename OutputIterator, typename value_type, int _Rank>
void copy(
    const array<value_type, _Rank>& _Src,
   OutputIterator _DestIter);

template <typename value_type, int _Rank>
void copy(
    const array<value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
void copy(
    const array_view<const value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
void copy(
    const array_view<value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
void copy(
    const array_view<const value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
void copy(
    const array_view<value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
void copy(
    InputIterator _SrcFirst,
    InputIterator _SrcLast,
    array_view<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
void copy(
    InputIterator _SrcFirst,
    array_view<value_type, _Rank>& _Dest);

template <typename OutputIterator, typename value_type, int _Rank>
void copy(
    const array_view<value_type, _Rank>& _Src,
    OutputIterator _DestIter);
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Объект для копирования.

*_DestIter*<br/>
Выходной итератор на начальную точку в месте назначения.

*InputIterator*<br/>
Тип итератора ввода.

*OutputIterator*<br/>
Тип итератора вывода.

*_Rank*<br/>
Ранг объекта, из которого производится копирование, или объект, в который производится копирование.

*_Src*<br/>
В объект для копирования.

*_SrcFirst*<br/>
Начальный итератор в исходный контейнер.

*_SrcLast*<br/>
Конечный итератор в исходный контейнер.

*value_type*<br/>
Тип данных копируемых элементов.

## <a name="copy_async"></a><a name="copy_async"></a> copy_async

Копирует объект C++ AMP и возвращает объект [completion_future](completion-future-class.md) , который можно ожидать. Нельзя копировать данные при выполнении кода в ускорителе.  Общая форма этой функции — `copy(src, dest)` .

```cpp
template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array<value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(InputIterator _SrcFirst, InputIterator _SrcLast,
    array<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(InputIterator _SrcFirst,
    array<value_type, _Rank>& _Dest);

template <typename OutputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array<value_type, _Rank>& _Src, OutputIterator _DestIter);

template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array<value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array_view<const value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array_view<value_type, _Rank>& _Src,
    array<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array_view<const value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array_view<value_type, _Rank>& _Src,
    array_view<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(InputIterator _SrcFirst, InputIterator _SrcLast,
    array_view<value_type, _Rank>& _Dest);

template <typename InputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(InputIterator _SrcFirst,
    array_view<value_type, _Rank>& _Dest);

template <typename OutputIterator, typename value_type, int _Rank>
concurrency::completion_future copy_async(
    const array_view<value_type, _Rank>& _Src, OutputIterator _DestIter);
```

### <a name="parameters"></a>Параметры

*_Dest*<br/>
Объект для копирования.

*_DestIter*<br/>
Выходной итератор на начальную точку в месте назначения.

*InputIterator*<br/>
Тип итератора ввода.

*OutputIterator*<br/>
Тип итератора вывода.

*_Rank*<br/>
Ранг объекта, из которого производится копирование, или объект, в который производится копирование.

*_Src*<br/>
В объект для копирования.

*_SrcFirst*<br/>
Начальный итератор в исходный контейнер.

*_SrcLast*<br/>
Конечный итератор в исходный контейнер.

*value_type*<br/>
Тип данных копируемых элементов.

### <a name="return-value"></a>Возвращаемое значение

Объект `future<void>` , который можно ожидать.

## <a name="direct3d_abort"></a><a name="direct3d_abort"></a> direct3d_abort

Прерывает выполнение функции с предложением ограничения `restrict(amp)` . Когда среда выполнения AMP обнаруживает вызов, она порождает исключение [runtime_exception](runtime-exception-class.md) с таким сообщением об ошибке: "Средство программной прорисовки: обнаружена инструкция прекращения работы шейдера".

```cpp
void direct3d_abort() restrict(amp);
```

## <a name="direct3d_errorf"></a><a name="direct3d_errorf"></a> direct3d_errorf

Выводит форматированную строку в окно вывода Visual Studio. Он вызывается из функции с `restrict(amp)` предложением ограничения. Когда среда выполнения AMP обнаруживает вызов, она вызывает исключение [runtime_exception](runtime-exception-class.md) с той же строкой форматирования.

```cpp
void direct3d_errorf(
    const char *,
...) restrict(amp);
```

## <a name="direct3d_printf"></a><a name="direct3d_printf"></a> direct3d_printf

Выводит форматированную строку в окно вывода Visual Studio. Он вызывается из функции с `restrict(amp)` предложением ограничения.

```cpp
void direct3d_printf(
    const char *,
...) restrict(amp);
```

## <a name="global_memory_fence"></a><a name="global_memory_fence"></a> global_memory_fence

Блокирует выполнение всех потоков в плитке до тех пор, пока не будут завершены все глобальные доступы к памяти. Это гарантирует, что доступ к глобальным памятьм будет виден другим потокам в плитке потока и выполнен в порядке программ.

```cpp
inline void global_memory_fence(const tile_barrier& _Barrier) restrict(amp);
```

### <a name="parameters"></a>Параметры

*_Barrier*<br/>
Объект tile_barrier

## <a name="parallel_for_each-function-c-amp"></a><a name="parallel_for_each"></a> Функция parallel_for_each (C++ AMP)

Выполняет функцию в домене вычислений. Дополнительные сведения см. в разделе [C++ amp Обзор](../../../parallel/amp/cpp-amp-overview.md).

```cpp
template <int _Rank, typename _Kernel_type>
void parallel_for_each(
    const extent<_Rank>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Dim0, int _Dim1, int _Dim2, typename _Kernel_type>
void parallel_for_each(
    const tiled_extent<_Dim0, _Dim1, _Dim2>& _Compute_domain,
   const _Kernel_type& _Kernel);

template <int _Dim0, int _Dim1, typename _Kernel_type>
void parallel_for_each(
    const tiled_extent<_Dim0, _Dim1>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Dim0, typename _Kernel_type>
void parallel_for_each(
    const tiled_extent<_Dim0>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Rank, typename _Kernel_type>
void parallel_for_each(
    const accelerator_view& _Accl_view,
    const extent<_Rank>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Dim0, int _Dim1, int _Dim2, typename _Kernel_type>
void parallel_for_each(
    const accelerator_view& _Accl_view,
    const tiled_extent<_Dim0, _Dim1, _Dim2>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Dim0, int _Dim1, typename _Kernel_type>
void parallel_for_each(
    const accelerator_view& _Accl_view,
    const tiled_extent<_Dim0, _Dim1>& _Compute_domain,
    const _Kernel_type& _Kernel);

template <int _Dim0, typename _Kernel_type>
void parallel_for_each(
    const accelerator_view& _Accl_view,
    const tiled_extent<_Dim0>& _Compute_domain,
    const _Kernel_type& _Kernel);
```

### <a name="parameters"></a>Параметры

*_Accl_view*<br/>
`accelerator_view`Объект для запуска параллельных вычислений.

*_Compute_domain*<br/>
`extent`Объект, содержащий данные для вычисления.

*_Dim0*<br/>
Измерение `tiled_extent` объекта.

*_Dim1*<br/>
Измерение `tiled_extent` объекта.

*_Dim2*<br/>
Измерение `tiled_extent` объекта.

*_Kernel*<br/>
Лямбда-или объект функции, который принимает аргумент типа "index \<_Rank> " и выполняет параллельное вычисление.

*_Kernel_type*<br/>
Лямбда-выражение или функтор.

*_Rank*<br/>
Ранг экстента.

## <a name="tile_static_memory_fence"></a><a name="tile_static_memory_fence"></a> tile_static_memory_fence

Блокирует выполнение всех потоков в плитке до тех пор, пока не будут завершены все необработанные `tile_static` доступ к памяти. Это гарантирует, что `tile_static` доступ к памяти будет виден другим потокам в плитке потока, и эти обращения будут выполняться в порядке программ.

```cpp
inline void tile_static_memory_fence(const tile_barrier& _Barrier) restrict(amp);
```

### <a name="parameters"></a>Параметры

*_Barrier*<br/>
Объект tile_barrier.

## <a name="see-also"></a>См. также раздел

[Пространство имен Concurrency (C++ AMP)](concurrency-namespace-cpp-amp.md)
