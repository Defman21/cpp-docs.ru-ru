---
description: Дополнительные сведения см. в разделе Пошаговое руководство. Реализация фьючерсов
title: Пошаговое руководство. Реализация фьючерсов
ms.date: 04/25/2019
helpviewer_keywords:
- implementing futures [Concurrency Runtime]
- futures, implementing [Concurrency Runtime]
ms.assetid: 82ea75cc-aaec-4452-b10d-8abce0a87e5b
ms.openlocfilehash: b2ea0b273f25ce42f8b177ce2d8e4b4aef195109
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97309229"
---
# <a name="walkthrough-implementing-futures"></a>Пошаговое руководство. Реализация фьючерсов

В этом разделе показано, как реализовать фьючерсы в приложении. В этом разделе показано, как объединить существующие функции в среда выполнения с параллелизмом в что-то, которое делает больше.

> [!IMPORTANT]
> В этом разделе рассматривается понятие фьючерсов для демонстрационных целей. Рекомендуется использовать [std:: future](../../standard-library/future-class.md) или [Concurrency:: Task](../../parallel/concrt/reference/task-class.md) , если требуется асинхронная задача, которая выполняет вычисление значения для последующего использования.

*Задача* — это вычисление, которое можно разложить на дополнительные, более детализированные вычисления. *Будущее* — это асинхронная задача, которая выполняет вычисление значения для последующего использования.

Для реализации фьючерсов в этом разделе определяется `async_future` класс. `async_future`Класс использует эти компоненты Среда выполнения с параллелизмом: класс [Concurrency:: task_group](reference/task-group-class.md) и класс [Concurrency:: single_assignment](../../parallel/concrt/reference/single-assignment-class.md) . `async_future`Класс использует `task_group` класс для асинхронного вычисления значения и `single_assignment` класс для хранения результата вычисления. Конструктор `async_future` класса принимает рабочую функцию, которая вычисляет результат, и `get` метод получает результат.

### <a name="to-implement-the-async_future-class"></a>Реализация класса async_future

1. Объявите класс шаблона с именем `async_future` , параметризованный для типа результирующего вычисления. Добавьте **`public`** **`private`** разделы и в этот класс.

[!code-cpp[concrt-futures#2](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_1.cpp)]

1. В **`private`** разделе `async_future` класса объявите `task_group` и элемент `single_assignment` данных.

[!code-cpp[concrt-futures#3](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_2.cpp)]

1. В **`public`** разделе `async_future` класса реализуйте конструктор. Конструктор является шаблоном, параметризованным в рабочей функции, которая выполняет вычисление результата. Конструктор асинхронно выполняет рабочую функцию в элементе `task_group` данных и использует функцию [Concurrency:: send](reference/concurrency-namespace-functions.md#send) для записи результата в `single_assignment` элемент данных.

[!code-cpp[concrt-futures#4](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_3.cpp)]

1. В **`public`** разделе `async_future` класса реализуйте деструктор. Деструктор ожидает завершения задачи.

[!code-cpp[concrt-futures#5](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_4.cpp)]

1. В **`public`** разделе `async_future` класса реализуйте `get` метод. Этот метод использует функцию [Concurrency:: Receive](reference/concurrency-namespace-functions.md#receive) для получения результата работы функции.

[!code-cpp[concrt-futures#6](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_5.cpp)]

## <a name="example"></a>Пример

### <a name="description"></a>Описание

В следующем примере показан полный `async_future` класс и пример его использования. `wmain`Функция создает объект std::[vector](../../standard-library/vector-class.md) , содержащий 10 000 случайных целочисленных значений. Затем он использует `async_future` объекты для поиска наименьших и максимальных значений, содержащихся в `vector` объекте.

### <a name="code"></a>Код

[!code-cpp[concrt-futures#1](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_6.cpp)]

### <a name="comments"></a>Комментарии

В этом примере выводятся следующие данные:

```Output
smallest: 0
largest:  9999
average:  4981
```

В примере используется `async_future::get` метод для получения результатов вычисления. `async_future::get`Метод ожидает завершения вычислений, если вычисления все еще активны.

## <a name="robust-programming"></a>Отказоустойчивость

Чтобы расширить `async_future` класс для обработки исключений, вызываемых рабочей функцией, измените `async_future::get` метод для вызова метода [concurrency:: task_group:: wait](reference/task-group-class.md#wait) . `task_group::wait`Метод создает исключения, созданные рабочей функцией.

В следующем примере показана измененная версия `async_future` класса. `wmain`Функция использует **`try`** - **`catch`** блок для вывода результата `async_future` объекта или для вывода значения исключения, созданного рабочей функцией.

[!code-cpp[concrt-futures-with-eh#1](../../parallel/concrt/codesnippet/cpp/walkthrough-implementing-futures_7.cpp)]

В этом примере выводятся следующие данные:

```Output
caught exception: error
```

Дополнительные сведения о модели обработки исключений в среда выполнения с параллелизмом см. в разделе [обработка исключений](../../parallel/concrt/exception-handling-in-the-concurrency-runtime.md).

## <a name="compiling-the-code"></a>Компиляция кода

Скопируйте пример кода и вставьте его в проект Visual Studio или вставьте в файл с именем, `futures.cpp` а затем выполните следующую команду в окне командной строки Visual Studio.

**cl.exe/EHsc фьючерсов. cpp**

## <a name="see-also"></a>См. также раздел

[среда выполнения с параллелизмом пошаговые руководства](../../parallel/concrt/concurrency-runtime-walkthroughs.md)<br/>
[Обработка исключений](../../parallel/concrt/exception-handling-in-the-concurrency-runtime.md)<br/>
[Класс task_group](reference/task-group-class.md)<br/>
[Класс single_assignment](../../parallel/concrt/reference/single-assignment-class.md)
