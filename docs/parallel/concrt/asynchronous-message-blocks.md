---
title: "Асинхронные блоки сообщений | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "нежадное объединение [среда выполнения с параллелизмом]"
  - "асинхронные блоки сообщений"
  - "жадное объединение [среда выполнения с параллелизмом]"
ms.assetid: 79c456c0-1692-480c-bb67-98f2434c1252
caps.latest.revision: 36
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
caps.handback.revision: 36
---
# Асинхронные блоки сообщений
[!INCLUDE[vs2017banner](../../assembler/inline/includes/vs2017banner.md)]

Библиотека агентов предоставляет несколько типов блоков сообщений, которые позволяют распространять сообщения среди компонентов приложений потокобезопасным способом. Эти типы блоков сообщений часто используются такие как с различные процедуры передачи сообщений, [concurrency::send](../Topic/send%20Function.md), [concurrency::asend](../Topic/asend%20Function.md), [concurrency::receive](../Topic/receive%20Function.md), и [concurrency::try_receive](../Topic/try_receive%20Function.md). Дополнительные сведения о процедурах, которые определяются библиотекой агентов передачи сообщений, см. в разделе [функции передачи сообщений](../../parallel/concrt/message-passing-functions.md).  
  
##  <a name="a-nametopa-sections"></a><a name="top"></a> Разделы  
 В этом разделе содержатся следующие подразделы.  
  
- [Источники и целевые объекты](#sources_and_targets)  
  
- [Распространение сообщений](#propagation)  
  
- [Обзор типов блоков сообщений](#overview)  
  
- [Класс unbounded_buffer](#unbounded_buffer)  
  
- [Класс overwrite_buffer](#overwrite_buffer)  
  
- [Класс single_assignment](#single_assignment)  
  
- [Call-класс](#call)  
  
- [Класс transformer](#transformer)  
  
- [Класс Choice](#choice)  
  
- [Классы соединения и multitype_join](#join)  
  
- [Класс Timer](#timer)  
  
- [Фильтрация сообщений](#filtering)  
  
- [Резервирование сообщений](#reservation)  
  
##  <a name="a-namesourcesandtargetsa-sources-and-targets"></a><a name="sources_and_targets"></a> Источники и целевые объекты  
 Источники и целевые объекты являются два важных участника передачи сообщений. A *источника* понимается конечная точка передачи данных, которая отправляет сообщения. A *целевой* понимается конечная точка передачи данных, которая получает сообщения. Можно представить источника в качестве конечной точки, из которой производится чтение, а целевой конечной точке, предназначенный для. Приложения подключаются источники и целевые объекты вместе форму *сети обмена сообщениями*.  
  
 Библиотека агентов использует два абстрактных классов для представления источников и целевых объектов: [concurrency::ISource](../../parallel/concrt/reference/isource-class.md) и [concurrency::ITarget](../../parallel/concrt/reference/itarget-class.md). Типы блоков сообщений, выполняющие роль источников, являются производными от `ISource`; типы блоков сообщений, выполняющие роль целевых объектов, являются производными от `ITarget`. Типы блоков сообщений, действующие в качестве источников и целевых объектов, наследуются от классов `ISource` и `ITarget`.  
  
 [[В начало](#top)]  
  
##  <a name="a-namepropagationa-message-propagation"></a><a name="propagation"></a> Распространение сообщений  
 *Сообщения* -это операция отправки сообщения из одного компонента. Когда блок сообщений предлагается сообщение, его можно принять, отклонить или отложить его. Типы блоков сообщений сохраняют и передают сообщения разными способами. Например `unbounded_buffer` класс хранит неограниченное число сообщений, `overwrite_buffer` класс хранит одно сообщение за раз, а класс transformer сохраняет измененную версию каждого сообщения. Эти типы блоков сообщений описаны более подробно далее в этом документе.  
  
 Когда блок сообщений принимает сообщение, он может при необходимости выполнения работы и, если блок сообщения является источником, передать обработанное сообщение другому члену сети. Блок сообщений можно использовать функцию фильтрации, чтобы отклонять сообщения, которые не нужно получать. Фильтры описаны более подробно далее в этом разделе, в разделе [фильтрации сообщений](#filtering). Блок сообщений, откладывающий сообщения можно зарезервировать сообщение и использовать его позже. Резервирование сообщений является более подробно далее в этом разделе, в разделе [резервирование сообщений](#reservation).  
  
 Библиотека агентов позволяет блокам сообщений асинхронно или синхронно передачи сообщений. При передаче сообщения в блок сообщений синхронно, например, с помощью `send` функции, среда выполнения блокирует текущий контекст, пока целевой блок принимает или отклоняет сообщение. При передаче сообщения в блок сообщений асинхронно, например, с помощью `asend` функции, среда выполнения предлагает сообщение целевому объекту, и если он принимает сообщение, планирует асинхронную задачу, распространяющую сообщение для получателя. Среда выполнения использует упрощенные задачи для распространения сообщений согласованным образом. Дополнительные сведения об упрощенных задачах см. в разделе [Планировщик](../../parallel/concrt/task-scheduler-concurrency-runtime.md).  
  
 Приложения подключаются источники и целевые объекты вместе сети обмена сообщениями. Обычно выполняется подключение к ней и вызов `send` или `asend` для передачи данных в сети. Для подключения к целевому объекту исходного блока сообщений, вызовите [concurrency::ISource::link_target](../Topic/ISource::link_target%20Method.md) метод. Отключение от целевой блок источника, вызовите [concurrency::ISource::unlink_target](../Topic/ISource::unlink_target%20Method.md) метод. Отключение от всех целевых системах блок источника, вызовите [concurrency::ISource::unlink_targets](../Topic/ISource::unlink_targets%20Method.md) метод. Когда один из предопределенных типов блоков сообщений покидает область или уничтожается, он автоматически отключает сам от любых целевых блоков. Некоторые типы блоков сообщений ограничить максимальное число целевых объектов, которые могут быть записаны. В следующем разделе описаны ограничения, которые применяются для предопределенных типов блоков сообщений.  
  
 [[В начало](#top)]  
  
##  <a name="a-nameoverviewa-overview-of-message-block-types"></a><a name="overview"></a> Обзор типов блоков сообщений  
 В следующей таблице кратко описывается роль типов важных блоков сообщений.  
  
 [unbounded_buffer](#unbounded_buffer)  
 Хранит очередь сообщений.  
  
 [overwrite_buffer](#overwrite_buffer)  
 Хранит одно сообщение, которое можно записать и многократно считывать.  
  
 [single_assignment](#single_assignment)  
 Хранит одно сообщение, которое можно один раз записать и многократно считывать.  
  
 [вызов](#call)  
 Выполняет работу при получении сообщения.  
  
 [transformer](#transformer)  
 Выполняет работу при получении данных и отправляет результат своей работы другому целевому блоку.  `transformer` Класс может действовать на различные входные и выходные типы.  
  
 [Выбор](#choice)  
 Выбирает первое доступное сообщение из набора источников.  
  
 [соединения и возвращаемым соединения](#join)  
 Подождите, пока все сообщения, полученные из набора источников и затем объединяет эти сообщения в одно сообщение для другого блока сообщений.  
  
 [таймер](#timer)  
 Отправляет сообщение в целевой блок через равные промежутки времени.  
  
 Эти типы блоков сообщений обладают различными характеристиками, делающими их полезными в различных ситуациях. Ниже перечислены некоторые характеристики:  
  
- *Тип распространения*: является ли блок сообщений выступает в качестве источника данных и приемником данных.  
  
- *Упорядочение сообщений*: сохраняет ли блок сообщений исходный порядок, отправленных или полученных сообщений. Каждый предопределенные типы блоков сообщений сохраняет исходный порядок, в котором отправляются или принимаются сообщения.  
  
- *Число источников*: максимальное число источников, из которых блок сообщений может производить чтение.  
  
- *Число целевых*: максимальное число целевых объектов, которые блок сообщений может производить запись.  
  
 Следующая таблица показывает, как эти характеристики соотносятся с различными типами блоков сообщений.  
  
|Тип блока сообщений|Тип распространения (источник, целевой или оба)|Упорядочение (Ordered или Unordered) сообщения|Число источников|Число целевых объектов|  
|------------------------|--------------------------------------------------|-----------------------------------------------|------------------|------------------|  
|`unbounded_buffer`|Оба значения|Ordered|Неограниченные|Неограниченные|  
|`overwrite_buffer`|Оба значения|Ordered|Неограниченные|Неограниченные|  
|`single_assignment`|Оба значения|Ordered|Неограниченные|Неограниченные|  
|`call`|целевого объекта|Ordered|Неограниченные|Не применимо|  
|`transformer`|Оба значения|Ordered|Неограниченные|1|  
|`choice`|Оба значения|Ordered|10|1|  
|`join`|Оба значения|Ordered|Неограниченные|1|  
|`multitype_join`|Оба значения|Ordered|10|1|  
|`timer`|Источник|Не применимо|Не применимо|1|  
  
 В следующих разделах описаны типы блоков сообщений, более подробно.  
  
 [[В начало](#top)]  
  
##  <a name="a-nameunboundedbuffera-unboundedbuffer-class"></a><a name="unbounded_buffer"></a> Класс unbounded_buffer  
  [Concurrency::unbounded_buffer](../Topic/unbounded_buffer%20Class.md) класс представляет структуру общего назначения асинхронного обмена сообщениями. В этом классе хранится очередь сообщений типа «первым вошел — первым вышел» (FIFO), в которую могут записывать данные несколько источников и из которой могут читать данные несколько целевых объектов. Если целевой объект получает сообщение от `unbounded_buffer` объекта, это сообщение удаляется из очереди сообщений. Таким образом несмотря на то что `unbounded_buffer` объект может иметь несколько целевых объектов, только один целевой объект получит каждое сообщение. Класс `unbounded_buffer` удобен, если нужно передать несколько сообщений другому компоненту и этот компонент должен принять каждое сообщение.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `unbounded_buffer` класса. Этот пример отправляет три значения `unbounded_buffer` объект а затем эти значения считываются из того же объекта.  
  
 [!code-cpp[concrt-unbounded_buffer-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_1.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
334455  
```  
  
 Полный пример, показывающий, как использовать `unbounded_buffer` см. в разделе [как: реализуют различные шаблоны производитель-получатель](../../parallel/concrt/how-to-implement-various-producer-consumer-patterns.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-nameoverwritebuffera-overwritebuffer-class"></a><a name="overwrite_buffer"></a> Класс overwrite_buffer  
  [Concurrency::overwrite_buffer](../../parallel/concrt/reference/overwrite-buffer-class.md) напоминает класс `unbounded_buffer` класса, за исключением того, что `overwrite_buffer` объект сохраняет только одно сообщение. Кроме того, когда целевой объект получает сообщение от `overwrite_buffer` объекта, это сообщение не удаляется из буфера. Поэтому копию сообщения могут получить несколько целевых объектов.  
  
  `overwrite_buffer` Класс полезен, когда требуется передать несколько сообщений другому компоненту, но этому компоненту нужно только самое последнее значение. Этот класс также может оказаться полезным при необходимости широковещательной передачи сообщения нескольким компонентам.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `overwrite_buffer` класса. Этот пример отправляет три значения `overwrite _buffer` объекта, затем текущее значение считывается с этого же объекта три раза. Этот пример похож на пример для `unbounded_buffer` класса. Однако `overwrite_buffer` Класс сохраняет только одно сообщение. Кроме того, среда выполнения не удаляет сообщение из `overwrite_buffer` объекта после его чтения.  
  
 [!CODE [concrt-overwrite_buffer-structure#1](../CodeSnippet/VS_Snippets_ConcRT/concrt-overwrite_buffer-structure#1)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
555555  
```  
  
 Полный пример, показывающий, как использовать `overwrite_buffer` см. в разделе [как: реализуют различные шаблоны производитель-получатель](../../parallel/concrt/how-to-implement-various-producer-consumer-patterns.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namesingleassignmenta-singleassignment-class"></a><a name="single_assignment"></a> Класс single_assignment  
  [Concurrency::single_assignment](../../parallel/concrt/reference/single-assignment-class.md) напоминает класс `overwrite_buffer` класса, за исключением того, что `single_assignment` объекта могут быть записаны только один раз. Как и в случае с классом `overwrite_buffer`, когда целевой объект получает сообщение от объекта `single_assignment`, это сообщение не удаляется. Поэтому копию сообщения могут получить несколько целевых объектов.  `single_assignment` Класс удобен при необходимости широковещательной передачи одного сообщения нескольким компонентам.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `single_assignment` класса. Этот пример отправляет три значения `single_assignment` объекта, затем текущее значение считывается с этого же объекта три раза. Этот пример похож на пример для `overwrite_buffer` класса. Хотя оба `overwrite_buffer` и `single_assignment` классы хранить одно сообщение, `single_assignment` класса можно записать только один раз.  
  
 [!code-cpp[concrt-single_assignment-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_2.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
333333  
```  
  
 Полный пример, показывающий, как использовать `single_assignment` см. в разделе [Пошаговое руководство: реализация фьючерсов](../../parallel/concrt/walkthrough-implementing-futures.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namecalla-call-class"></a><a name="call"></a> Call-класс  
  [Concurrency::call](../../parallel/concrt/reference/call-class.md) класс действует как получатель сообщения, которое выполняет рабочую функцию при получении данных. Эта рабочая функция может быть лямбда-выражение, объект функции или указатель функции. A `call` объекта отличается от обычного вызова функции, так как он действует параллельно с другими компонентами, отправляющими ему сообщения. Если `call` объект выполняет работу, когда он получает сообщение, он добавляет это сообщение в очередь. Каждый `call` объект обрабатывает сообщения в порядке их получения из очереди.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `call` класса. В этом примере создается `call` объект, который выводит все значения, получаемые на консоль. В примере затем отправляется три значения `call` объект. Так как `call` объект обрабатывает сообщения в отдельном потоке, в этом примере также используется переменная счетчика и [событие](../Topic/event%20Class.md) объекта, чтобы убедиться, что `call` объект обрабатывает все сообщения, прежде чем `wmain` возврата функцией.  
  
 [!code-cpp[concrt-call-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_3.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
334455  
```  
  
 Полный пример, показывающий, как использовать `call` см. в разделе [как: предоставления рабочих функций классам call и transformer](../../parallel/concrt/how-to-provide-work-functions-to-the-call-and-transformer-classes.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-nametransformera-transformer-class"></a><a name="transformer"></a> Класс transformer  
  [Concurrency::transformer](../../parallel/concrt/reference/transformer-class.md) класс действует как получателя, так и как отправителя сообщения.  `transformer` Напоминает класс `call` класса, так как он выполняет определяемые пользователем рабочую функцию при получении данных. Однако `transformer` класс также отправляет результат выполнения рабочей функции объектам-получателям. Как `call` объекта, `transformer` объект работает параллельно с другими компонентами, отправляющими ему сообщения. Если `transformer` объект выполняет работу, когда он получает сообщение, он добавляет это сообщение в очередь. Каждый `transformer` объект обрабатывает сообщения из своей очереди в порядке их получения.  
  
  `transformer` Класс отправляет свои сообщения одному целевому объекту. Если задать `_PTarget` параметр в конструкторе `NULL`, позже можно указать целевой объект, вызвав [concurrency::link_target](../Topic/source_block::link_target%20Method.md) метод.  
  
 В отличие от всех других асинхронных типов блоков сообщений, предоставляемых библиотекой агентов `transformer` класс может действовать на различные входные и выходные типы. Эта способность преобразовывать данные из одного типа в другой превращает `transformer` класса ключевой компонент многих параллельных сетей. Кроме того, можно добавить возможность параллельной обработки более детальный уровень в функции рабочих `transformer` объекта.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `transformer` класса. В этом примере создается `transformer` объекта, умножающий все введенные `int` значение на 0,33, чтобы получить `double` значение как выходные данные. Затем пример получает преобразованные значения из того же `transformer` объекта и выводит их на консоль.  
  
 [!code-cpp[concrt-transformer-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_4.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
10.8914.5218.15  
```  
  
 Полный пример, показывающий, как использовать `transformer` см. в разделе [Практическое руководство: использование преобразователя в конвейере данных](../../parallel/concrt/how-to-use-transformer-in-a-data-pipeline.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namechoicea-choice-class"></a><a name="choice"></a> Класс Choice  
  [Concurrency::choice](../../parallel/concrt/reference/choice-class.md) класс выбирает первое доступное сообщение из набора источников.  `choice` Класс представляет механизм потока управления вместо механизма потока данных (раздел [Asynchronous Agents Library](../../parallel/concrt/asynchronous-agents-library.md) описаны различия между потока данных и потока управления).  
  
 Чтение из объекта choice похоже на вызов функции Windows API `WaitForMultipleObjects` при `bWaitAll` параметра `FALSE`. Однако `choice` класс привязывает данные к самому событию, вместо ко внешнему объекту синхронизации.  
  
 Как правило, используется `choice` класса вместе с [concurrency::receive](../Topic/receive%20Function.md) функцию для использования потока управления в приложении. Используйте `choice` класса, если требуется выбирать между буферами сообщений, имеющих различные типы. Используйте `single_assignment` класса, если требуется выбирать между буферами сообщений, имеют одинаковый тип.  
  
 Порядок, в котором связывания источников с `choice` объекта важно, так как он определяет выбираемое сообщение. Например, рассмотрим случай, где связать несколько буферов сообщений, которые уже содержат сообщение `choice` объекта.  `choice` Объект выбирает сообщение из первого связанного с ним источника. После привязки всех источников `choice` сохраняет порядок, в котором каждый из источников получает сообщение.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `choice` класса. В этом примере используется [concurrency::make_choice](../Topic/make_choice%20Function.md) функцию для создания `choice` объекта, который выбирает среди трех блоков сообщений. Затем в примере вычисляются различные числа Фибоначчи и каждый результат сохраняется в отдельном блоке сообщений. В примере затем выводится на консоль сообщение, основанное на первой завершившейся операции.  
  
 [!code-cpp[concrt-choice-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_5.cpp)]  
  
 Этот пример выдает следующий результат:  
  
```Output  
fib35 received its value first. Result = 9227465  
```  
  
 Так как задача, вычисляющая 35<sup>й</sup> Фибоначчи не обязательно завершится первой, результат этого примера может варьироваться.  
  
 В этом примере используется [concurrency::parallel_invoke](../Topic/parallel_invoke%20Function.md) алгоритм для вычисления чисел Фибоначчи параллельно. Дополнительные сведения о `parallel_invoke`, в разделе [Параллельные алгоритмы](../Topic/Parallel%20Algorithms.md).  
  
 Полный пример, показывающий, как использовать `choice` см. в разделе [как: Выбор между завершения задач](../../parallel/concrt/how-to-select-among-completed-tasks.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namejoina-join-and-multitypejoin-classes"></a><a name="join"></a> Классы соединения и multitype_join  
  [Concurrency::join](../Topic/join%20Class.md) и [concurrency::multitype_join](../../parallel/concrt/reference/multitype-join-class.md) классы позволяют ожидать, пока каждый элемент набора источников для получения сообщения.  `join` Класс предназначен для объектов-источников, имеющих общий тип сообщений.  `multitype_join` Класс предназначен для объектов-источников, имеющих разные типы сообщений.  
  
 Чтение из `join` или `multitype_join` похоже на вызов функции Windows API `WaitForMultipleObjects` при `bWaitAll` параметра `TRUE`. Однако, как `choice` объект, `join` и `multitype_join` объекты используют механизм событий, который привязывает данные к самому событию, вместо ко внешнему объекту синхронизации.  
  
 Чтение из `join` создается std::[вектор](vector%20Class.md) объекта. Чтение из `multitype_join` создается std::[кортеж](../../standard-library/tuple-class.md) объекта. Элементы располагаются в этих объектах в том же порядке, как их соответствующие буферы источника связаны с `join` или `multitype_join` объекта. Поскольку порядок, в котором связать источник буферов для `join` или `multitype_join` объект связан с порядком элементов в итоговом объекте `vector` или `tuple` объекта, рекомендуется не отсоединять существующий исходный буфер от соединения. Это может привести к неопределенному поведению.  
  
### <a name="greedy-versus-non-greedy-joins"></a>Жадного и нежадные объединения  
  `join` И `multitype_join` классы поддерживают концепцию жадных и нежадных объединений. A *жадное объединение* принимает сообщения от каждого из своих источников сообщений станут доступны, пока не будут доступны все сообщения. A *нежадное объединение* получает сообщения в два этапа. Во-первых нежадное объединение ожидает, пока не предлагается сообщение от каждого из своих источников. Во-вторых все исходные сообщения доступны, нежадное соединение пытается зарезервировать все эти сообщения. Если оно может зарезервировать все сообщения, он получает все сообщения и распространяет их цели. В противном случае — он освобождает, или отменяет резервирование сообщений и снова ожидает каждый источник для получения сообщения.  
  
 Жадное объединение работает лучше, чем нежадные объединения, поскольку сообщения принимаются немедленно. Тем не менее в редких случаях жадные соединения может привести к взаимоблокировкам. Используйте нежадное объединение при наличии нескольких объединений, содержащих один или несколько общих объектов-источников.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `join` класса. В этом примере используется [concurrency::make_join](../Topic/make_join%20Function.md) функцию для создания `join` объект, получающий от трех `single_assignment` объектов. В этом примере вычисляются различные числа Фибоначчи, и каждый результат сохраняется в другом `single_assignment` объекта, а затем выводит на консоль результаты, `join` содержащиеся в объекте. Этот пример похож на пример для `choice` класса, за исключением того, что `join` класс ожидает все исходные блоки сообщений для получения сообщения.  
  
 [!code-cpp[concrt-join-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_6.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
fib35 = 9227465fib37 = 24157817half_of_fib42 = 1.33957e+008  
```  
  
 В этом примере используется [concurrency::parallel_invoke](../Topic/parallel_invoke%20Function.md) алгоритм для вычисления чисел Фибоначчи параллельно. Дополнительные сведения о `parallel_invoke`, в разделе [Параллельные алгоритмы](../Topic/Parallel%20Algorithms.md).  
  
 Полные примеры, которые демонстрируют использование `join` см. в разделе [как: Выбор между завершения задач](../../parallel/concrt/how-to-select-among-completed-tasks.md) и [Пошаговое руководство: использование класса join для предотвращения взаимоблокировок](../../parallel/concrt/walkthrough-using-join-to-prevent-deadlock.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-nametimera-timer-class"></a><a name="timer"></a> Класс Timer  
 Параллелизм::[класс timer](../../parallel/concrt/reference/timer-class.md) выступает в качестве источника сообщения. A `timer` объекта отправляет сообщение целевому объекту после истечения указанного периода времени.  `timer` Класс полезен, если требуется задержать передачу сообщения или требуется передавать сообщения через постоянные интервалы времени.  
  
  `timer` Класс отправляет свое сообщение только одному целевому объекту. Если задать `_PTarget` параметр в конструкторе `NULL`, позже можно указать целевой объект, вызвав [concurrency::ISource::link_target](../Topic/source_block::link_target%20Method.md) метод.  
  
 Объект `timer` может быть повторяющимся или неповторяющимся. Чтобы создать повторяющийся таймер, передайте `true` для `_Repeating` параметра при вызове конструктора. В противном случае, передайте `false` для `_Repeating` для создания неповторяющегося таймера. Если таймер повторяющийся, он отправляет одного сообщения адресату после каждого интервала.  
  
 Библиотека агентов создает `timer` объекты в незапущенном состоянии. Чтобы запустить объект таймера, вызовите [Concurrency::Timer:: Start](../Topic/timer::start%20Method.md) метод. Чтобы остановить `timer` объекта, уничтожить объект или вызов [concurrency::timer::stop](../Topic/timer::stop%20Method.md) метод. Чтобы приостановить повторяющийся таймер, вызовите [concurrency::timer::pause](../Topic/timer::pause%20Method.md) метод.  
  
### <a name="example"></a>Пример  
 В следующем примере показана базовая структура работы с `timer` класса. В примере используется `timer` и `call` объектов, чтобы сообщить о ходе выполнения длительной операции.  
  
 [!code-cpp[concrt-timer-structure#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_7.cpp)]  
  
 Этот пример выдает следующий результат:  
  
```Output  
Computing fib(42)..................................................result is 267914296  
```  
  
 Полный пример, показывающий, как использовать `timer` см. в разделе [как: передавать сообщения через постоянные интервалы времени](../../parallel/concrt/how-to-send-a-message-at-a-regular-interval.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namefilteringa-message-filtering"></a><a name="filtering"></a> Фильтрация сообщений  
 При создании объекта блока сообщений можно предоставить *функция filter* определяет ли блок сообщений принимает или отклоняет сообщение. Функция фильтрации является удобным способом гарантировать, что блок сообщений получать только определенные значения.  
  
 Следующий пример демонстрирует создание `unbounded_buffer` объект, который использует функцию фильтрации, чтобы принимать только четные числа.  `unbounded_buffer` Объект отклоняет нечетных чисел и таким образом не распространяет нечетных чисел его целевым блокам.  
  
 [!code-cpp[concrt-filter-function#1](../../parallel/concrt/codesnippet/CPP/asynchronous-message-blocks_8.cpp)]  
  
 В этом примере выводятся следующие данные:  
  
```Output  
0 2 4 6 8  
```  
  
 Функция filter может быть лямбда-функции, указателя функции или объекта функции. Любая функция фильтрации принимает одну из следующих форм.  
  
```Output  
bool (T)  
bool (T const &)  
```  
  
 Чтобы исключить лишнее копирование данных, следует используйте вторую форму при наличии Агрегатный тип, передаваемый по значению.  
  
 Поддержка фильтрации сообщений *потока данных* модель программирования, в которой компоненты выполняют вычисления при получении данных. Примеры использования функций фильтрации для управления потоком данных в сети передачи сообщений см. в разделе [Практическое руководство: использование фильтра блока сообщений](../../parallel/concrt/how-to-use-a-message-block-filter.md), [Пошаговое руководство: создание агента потоков данных](../Topic/Walkthrough:%20Creating%20a%20Dataflow%20Agent.md), и [Пошаговое руководство: создание сети обработки изображений](../../parallel/concrt/walkthrough-creating-an-image-processing-network.md).  
  
 [[В начало](#top)]  
  
##  <a name="a-namereservationa-message-reservation"></a><a name="reservation"></a> Резервирование сообщений  
 *Резервирование сообщений* позволяет блоку сообщений зарезервировать сообщение для последующего использования. Как правило резервирование сообщений не используется напрямую. Однако понимание сообщения резервирования помогут вам лучше понять поведение некоторых предопределенных типов блоков сообщений.  
  
 Рассмотрим жадные и нежадные соединения. Они используют резервирование сообщений резервирование сообщений для последующего использования. Как описано ранее, нежадное соединение получает сообщения в два этапа. Во время первой фазы нежадный `join` объект ожидает от каждого из своих источников для получения сообщения. Нежадное соединение пытается зарезервировать все эти сообщения. Если оно может зарезервировать все сообщения, он получает все сообщения и распространяет их цели. В противном случае — он освобождает, или отменяет резервирование сообщений и снова ожидает каждый источник для получения сообщения.  
  
 Жадное соединение, также считывающее входящие сообщения из нескольких источников, использует резервирование сообщений, чтобы считывать дополнительные сообщения, время ожидания получения сообщения из каждого источника. Например, рассмотрим жадное соединение, получающее сообщения от блоков сообщений `A` и `B`. Если жадное соединение получает два сообщения из B, но еще не получил сообщение от `A`, жадное объединение сохраняет уникальный идентификатор сообщения для второе сообщение от `B`. После жадное соединение получает сообщение от `A` и распространяет эти сообщения, оно использует сохраненный идентификатор сообщения ли второе сообщение от `B` по-прежнему доступен.  
  
 Резервирование сообщений можно использовать при реализации собственных типов блоков пользовательское сообщение. Пример о том, как создать пользовательский тип блока сообщений см. в разделе [Пошаговое руководство: Создание пользовательского блока сообщений](../Topic/Walkthrough:%20Creating%20a%20Custom%20Message%20Block.md).  
  
 [[В начало](#top)]  
  
## <a name="see-also"></a>См. также раздел  
 [Библиотека асинхронных агентов](../../parallel/concrt/asynchronous-agents-library.md)
