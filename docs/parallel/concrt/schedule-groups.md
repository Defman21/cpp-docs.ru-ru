---
description: 'Дополнительные сведения о: группы расписаний'
title: Группы расписаний
ms.date: 11/04/2016
helpviewer_keywords:
- schedule groups
ms.assetid: 03523572-5891-4d17-89ce-fa795605f28b
ms.openlocfilehash: bee4f20ae58f94ddad93770232028df7b82dd39e
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97188070"
---
# <a name="schedule-groups"></a>Группы расписаний

В этом документе описывается роль групп расписаний в среда выполнения с параллелизмом. *Группа расписаний* аффинитизес или группирует связанные задачи вместе. У каждого планировщика есть одна или несколько групп расписаний. Используйте группы расписаний, когда требуется высокая степень локальности связанных задач, например если группу связанных задач лучше выполнять в одном узле процессора. И наоборот, используйте экземпляры планировщика, если приложение имеет определенные требования к качеству, например, если требуется ограничить объем вычислительных ресурсов, выделенных для набора задач. Дополнительные сведения об экземплярах планировщика см. в разделе [экземпляры планировщика](../../parallel/concrt/scheduler-instances.md).

> [!TIP]
> Среда выполнения с параллелизмом предоставляет планировщик по умолчанию, и таким образом не требуется создавать планировщик в приложении. Поскольку планировщик задач помогает точно настроить производительность приложений, рекомендуется начать с [библиотеки параллельных шаблонов (PPL)](../../parallel/concrt/parallel-patterns-library-ppl.md) или [библиотеки асинхронных агентов](../../parallel/concrt/asynchronous-agents-library.md) , если вы не знакомы с среда выполнения с параллелизмом.

Каждый `Scheduler` объект имеет группу расписаний по умолчанию для каждого узла планирования. *Узел планирования* сопоставляется с базовой топологией системы. Среда выполнения создает один узел планирования для каждого пакета процессора или узла NUMA, в зависимости от того, какое значение больше. Если не связать явно задачу с группой расписаний, планировщик выбирает, в какую группу добавить задачу.

`SchedulingProtocol`Политика планировщика влияет на порядок, в котором планировщик выполняет задачи в каждой группе расписаний. Если `SchedulingProtocol` для задано значение `EnhanceScheduleGroupLocality` (по умолчанию), планировщик задач выбирает следующую задачу из группы расписаний, в которой она работает, когда текущая задача завершается или совместно выдается. Планировщик задач просматривает текущую группу расписаний для работы перед переходом к следующей доступной группе. И наоборот, если параметр `SchedulingProtocol` имеет значение `EnhanceForwardProgress` , планировщик переходит к следующей группе расписаний после завершения каждой задачи или ее возврата. Пример, сравнивающий эти политики, см. в разделе [как использовать группы расписаний для влияния на порядок выполнения](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md).

Среда выполнения использует класс [Concurrency:: ScheduleGroup](../../parallel/concrt/reference/schedulegroup-class.md) для представления групп расписаний. Чтобы создать `ScheduleGroup` объект, вызовите метод [Concurrency:: CurrentScheduler:: CreateScheduleGroup](reference/currentscheduler-class.md#createschedulegroup) или [Concurrency:: Scheduler:: CreateScheduleGroup](reference/scheduler-class.md#createschedulegroup) . Среда выполнения использует механизм подсчета ссылок для управления жизненным циклом `ScheduleGroup` объектов точно так же, как и с `Scheduler` объектами. При создании `ScheduleGroup` объекта среда выполнения устанавливает для счетчика ссылок значение 1. Метод [Concurrency:: ScheduleGroup:: Reference](reference/schedulegroup-class.md#reference) увеличивает счетчик ссылок на единицу. Метод [Concurrency:: ScheduleGroup:: Release](reference/schedulegroup-class.md#release) уменьшает значение счетчика ссылок на единицу.

Многие типы в среда выполнения с параллелизмом позволяют связать объект с группой расписаний. Например, классы [Concurrency:: Agent](../../parallel/concrt/reference/agent-class.md) и блоки сообщений, такие как [concurrency:: unbounded_buffer](reference/unbounded-buffer-class.md), [Concurrency:: Join](../../parallel/concrt/reference/join-class.md)и Concurrency::[Timer](reference/timer-class.md), предоставляют перегруженные версии конструктора, которые принимают `ScheduleGroup` объект. Среда выполнения использует `Scheduler` объект, связанный с этим объектом, `ScheduleGroup` для планирования задачи.

Можно также использовать метод [Concurrency:: ScheduleGroup:: ScheduleTask](reference/schedulegroup-class.md#scheduletask) , чтобы запланировать упрощенную задачу. Дополнительные сведения о упрощенных задачах см. в разделе [упрощенные задачи](../../parallel/concrt/lightweight-tasks.md).

## <a name="example"></a>Пример

Пример использования групп расписаний для управления порядком выполнения задач см. [в разделе как использовать группы расписаний для влияния на порядок выполнения](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md).

## <a name="see-also"></a>См. также раздел

[Планировщик заданий](../../parallel/concrt/task-scheduler-concurrency-runtime.md)<br/>
[Экземпляры планировщика](../../parallel/concrt/scheduler-instances.md)<br/>
[Как использовать группы расписаний для влияния на порядок выполнения](../../parallel/concrt/how-to-use-schedule-groups-to-influence-order-of-execution.md)
