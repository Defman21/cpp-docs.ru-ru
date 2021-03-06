---
description: Дополнительные сведения см. в статье как использовать обработку исключений для прерывания работы параллельного цикла.
title: Практическое руководство. Использование обработки исключений для выхода из параллельного цикла
ms.date: 11/04/2016
helpviewer_keywords:
- search algorithm, writing [Concurrency Runtime]
- writing a search algorithm [Concurrency Runtime]
ms.assetid: 16d7278c-2d10-4014-9f58-f1899e719ff9
ms.openlocfilehash: aedad8f5851a606b91894ea07fce7e666d307992
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97334680"
---
# <a name="how-to-use-exception-handling-to-break-from-a-parallel-loop"></a>Практическое руководство. Использование обработки исключений для выхода из параллельного цикла

В этом разделе показано, как написать алгоритм поиска для простой древовидной структуры.

В разделе [Отмена](cancellation-in-the-ppl.md) статьи объясняется роль отмены в библиотеке параллельных шаблонов. Использование обработки исключений является менее эффективным способом отмены параллельной работы, чем использование методов [Concurrency:: task_group:: Cancel](reference/task-group-class.md#cancel) и [concurrency:: structured_task_group:: Cancel](reference/structured-task-group-class.md#cancel) . Однако одним из сценариев, в которых используется обработка исключений для отмены работы, является ситуация, когда вы вызываете библиотеку стороннего производителя, которая использует задачи или параллельные алгоритмы, но не `task_group` предоставляет `structured_task_group` объект или для отмены.

## <a name="example-basic-tree-type"></a>Пример: базовый тип дерева

В следующем примере показан базовый `tree` тип, содержащий элемент данных и список дочерних узлов. В следующем разделе показан текст `for_all` метода, который рекурсивно выполняет рабочую функцию на каждом дочернем узле.

[!code-cpp[concrt-task-tree-search#2](../../parallel/concrt/codesnippet/cpp/how-to-use-exception-handling-to-break-from-a-parallel-loop_1.cpp)]

## <a name="example-perform-work-in-parallel"></a>Пример. Параллельное выполнение работы

В следующем примере показан `for_all` метод. В нем используется алгоритм [параллелизма::p arallel_for_each](reference/concurrency-namespace-functions.md#parallel_for_each) для выполнения рабочей функции на каждом узле дерева параллельно.

[!code-cpp[concrt-task-tree-search#1](../../parallel/concrt/codesnippet/cpp/how-to-use-exception-handling-to-break-from-a-parallel-loop_2.cpp)]

## <a name="example--search-the-tree-for-a-value"></a>Пример. Поиск значения в дереве

В следующем примере показана функция `search_for_value`, которая выполняет поиск значения в предоставленном объекте `tree`. Эта функция передает в `for_all` метод рабочую функцию, которая создает исключение при обнаружении узла дерева, содержащего указанное значение.

Предположим, что `tree` класс предоставляется сторонней библиотекой и не может быть изменен. В этом случае целесообразно использовать обработку исключений, так как `for_all` метод не предоставляет `task_group` `structured_task_group` объект или для вызывающего объекта. Таким образом, Рабочая функция не может напрямую отменять родительскую группу задач.

Когда Рабочая функция, предоставляемая группе задач, вызывает исключение, среда выполнения останавливает все задачи, которые находятся в группе задач (включая все дочерние группы задач), и удаляет все задачи, которые еще не запущены. `search_for_value`Функция использует **`try`** - **`catch`** блок для захвата исключения и вывода результата на консоль.

[!code-cpp[concrt-task-tree-search#3](../../parallel/concrt/codesnippet/cpp/how-to-use-exception-handling-to-break-from-a-parallel-loop_3.cpp)]

## <a name="example-create-and-search-a-tree-in-parallel"></a>Пример: параллельное создание и поиск в дереве

В следующем примере создается `tree` объект и выполняется поиск нескольких значений в параллельном режиме. `build_tree`Эта функция показана далее в этом разделе.

[!code-cpp[concrt-task-tree-search#4](../../parallel/concrt/codesnippet/cpp/how-to-use-exception-handling-to-break-from-a-parallel-loop_4.cpp)]

В этом примере используется алгоритм [arallel_invoke Concurrency::p](reference/concurrency-namespace-functions.md#parallel_invoke) для параллельного поиска значений. Дополнительные сведения об этом алгоритме см. в разделе [Параллельные алгоритмы](../../parallel/concrt/parallel-algorithms.md).

## <a name="example-finished-exception-handling-code-sample"></a>Пример. завершенный пример кода обработки исключений

В следующем полном примере используется обработка исключений для поиска значений в простой древовидной структуре.

[!code-cpp[concrt-task-tree-search#5](../../parallel/concrt/codesnippet/cpp/how-to-use-exception-handling-to-break-from-a-parallel-loop_5.cpp)]

В этом примере выводится следующий пример выходных данных.

```Output
Found a node with value 32614.
Found a node with value 86131.
Did not find node with value 17522.
```

## <a name="compiling-the-code"></a>Компиляция кода

Скопируйте пример кода и вставьте его в проект Visual Studio или вставьте в файл с именем, `task-tree-search.cpp` а затем выполните следующую команду в окне командной строки Visual Studio.

> **cl.exe/EHsc ТАСК-три-СЕАРЧ. cpp**

## <a name="see-also"></a>См. также раздел

[Отмена в библиотеке параллельных шаблонов](cancellation-in-the-ppl.md)<br/>
[Обработка исключений](../../parallel/concrt/exception-handling-in-the-concurrency-runtime.md)<br/>
[Параллельное выполнение задач](../../parallel/concrt/task-parallelism-concurrency-runtime.md)<br/>
[Параллельные алгоритмы](../../parallel/concrt/parallel-algorithms.md)<br/>
[Класс task_group](reference/task-group-class.md)<br/>
[Класс structured_task_group](../../parallel/concrt/reference/structured-task-group-class.md)<br/>
[Функция parallel_for_each](reference/concurrency-namespace-functions.md#parallel_for_each)
