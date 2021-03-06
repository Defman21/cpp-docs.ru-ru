---
title: Справочные материалы. Представления Windows Performance Analyzer
description: Справочник по представлениям Аналитики сборок C++, доступным в Windows Performance Analyzer.
ms.date: 11/03/2019
helpviewer_keywords:
- C++ Build Insights
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: 2ad5d2153fdf434461e1af982e9d9f343e9957a9
ms.sourcegitcommit: 9c2b3df9b837879cd17932ae9f61cdd142078260
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "92919505"
---
# <a name="reference-windows-performance-analyzer-views"></a>Справочные материалы. Представления Windows Performance Analyzer

::: moniker range="<=msvc-150"

Средства C++ Build Insights доступны в Visual Studio 2019. Чтобы отобразилась документация для этой версии, установите в этой статье селектор **Версия** Visual Studio в положение "Visual Studio 2019". Он находится в верхней части оглавления на этой странице.

::: moniker-end
::: moniker range="msvc-160"

В этой статье приводятся подробные сведения обо всех представлениях Аналитики сборок C++, которые доступны в Windows Performance Analyzer (WPA). На этой странице можно найти:

- описания столбцов данных;
- доступные предустановки для каждого представления, включая сведения о предполагаемом использовании и предпочтительном режиме просмотра.

Если вы еще не знакомы с WPA, мы рекомендуем сначала узнать об [использовании WPA с Аналитикой сборок C++](../tutorials/wpa-basics.md).

## <a name="build-explorer"></a>Обозреватель сборок

Представление обозревателя сборок поддерживает следующие возможности:

- диагностика проблем с параллелизмом;
- определение наиболее длительной части процесса сборки (синтаксический анализ, создание кода или компоновка);
- определение узких мест и необычно длительных операций сборки.

### <a name="build-explorer-view-data-columns"></a>Столбцы данных в представлении обозревателя сборки

| Имя столбца | Описание |
|-|-|
| BuildTimelineDescription | Текстовое описание временной шкалы, к которой относится текущее действие или свойство. |
| BuildTimelineId          | Порядковый индекс (начиная с нуля) для временной шкалы, к которой относится текущее действие или свойство. |
| Компонент                | Компонент, который компилируется или компонуется в момент создания текущего события. Этот столбец имеет значение *\<Invocation X Info\>* , если с текущим событием не связан ни один компонент. X — уникальный числовой идентификатор вызова, выполняемого в момент возникновения события. Этот идентификатор совпадает со значением в столбце InvocationId для этого события. |
| Count                    | Число действий или свойств, представленных этой строкой данных. Это значение всегда равно 1 и применимо только в сценариях статистической обработки при группировке нескольких строк. |
| ExclusiveCPUTime         | Время ЦП в миллисекундах, использованное текущим действием. Это значение не включает время, затраченное на дочерние действия. |
| ExclusiveDuration        | Длительность действия в миллисекундах. Это значение не включает время, затраченное на дочерние действия. |
| InclusiveCPUTime         | Время ЦП в миллисекундах, использованное текущим действием и всеми его дочерними действиями. |
| InclusiveDuration        | Длительность действия в миллисекундах, включая все его дочерние действия. |
| InvocationDescription    | Текстовое описание вызова, в котором произошло это событие. Это описание содержит сведения о файле *cl.exe* или *link.exe* и уникальный числовой идентификатор вызова. Если применимо, здесь указывается полный путь к компоненту, который компилируется или компонуется во время этого вызова. Для вызовов, которые не компилируют ни одного компонента или компилируют несколько компонентов, этот путь содержит пустое значение. Идентификатор вызова совпадает со значением в столбце InvocationId для этого события. |
| InvocationId             | Уникальный числовой идентификатор для вызова, в котором возникло текущее событие. |
| Имя                     | Имя действия или свойства, представленного этим событием. |
| Time                     | Отметка времени, которая указывает, когда произошло событие. |
| Инструмент                     | Средство, которое выполнялось при возникновении этого события. Этот столбец имеет значение CL либо Link. |
| Тип                     | Тип текущего события. Здесь возможны значения Activity и Property. |
| Значение                    | Если текущее событие является свойством, этот столбец содержит его значение. Столбец остается пустым, если текущее событие является действием. |

### <a name="build-explorer-view-presets"></a>Предустановки для представления обозревателя сборки

| Имя предустановки           | Предпочтительный режим просмотра | Использование |
|-----------------------|---------------------|------------|
| Статистика действий   | График или таблица       | Эта предустановка позволяет просмотреть агрегированную статистику по всем действиям в обозревателе сборки. В режиме таблицы вы можете сразу увидеть, какая часть процесса сборки (синтаксический анализ, создание кода или компоновка) выполняется слишком долго. Для каждого действия отображается общая длительность с сортировкой в порядке убывания. Вы можете открыть подробные сведения, щелкнув узел верхнего уровня, чтобы просмотреть все вызовы за период выполнения самых длительных действий. При желании вы можете изменить параметры WPA, чтобы отображать средние значения или другие агрегаты. В режиме графика вы видите, в какой момент активируется какое действие сборки. |
| Вызовы           | График               | Вы можете прокрутить список вызовов в представлении графика с сортировкой по времени запуска. Эта возможность в сочетании с представлением загрузки ЦП (с выборкой) позволяет найти вызовы, обработка которых выполнялась в период высокой загрузки ЦП. Так вы определите проблемы с параллелизмом. |
| Свойства вызова | Таблица               | Вы можете быстро найти важную информацию о конкретном вызове компилятора или компоновщика, а также узнать версию средства, рабочую папку или полную командную строку, которой оно было вызвано. |
| График выполнения процессов             | График               | Вы можете просмотреть график параллельной обработки сборки, быстро определить проблемы с параллелизмом и узкие места, настроить WPA для выбора другого значения столбцов в соответствии со своими задачами, а также выбрать описания вызовов в качестве последнего столбца с группировкой, чтобы просмотреть гистограмму всех вызовов с цветовым кодированием. Так вам будет проще быстро найти причины потери времени. После этого можно увеличить масштаб и выбрать имя действия в качестве последнего столбца с группировкой, чтобы увидеть самые длительно выполняющиеся части процесса. |

## <a name="files"></a>Файлы

Представление файлов позволяет выполнить следующее:

- определить, какие заголовки добавляются чаще других;
- выбрать, что следует включать в предкомпилированный заголовок (PCH).

### <a name="files-view-data-columns"></a>Столбцы данных в представлении файлов

| Имя столбца              | Описание |
|--------------------------|-------------|
| ActivityName             | Действие, которое выполнялось во время создания текущего файлового события. Пока здесь возможно только одно значение: *Parsing*. |
| BuildTimelineDescription | * |
| BuildTimelineId          | * |
| Компонент                | * |
| Count                    | * |
| Глубина                    | Положение в дереве включений (начиная с нуля), в котором располагается файл. Отсчет начинается от корневого элемента дерева включений. Значение 0 обычно соответствует файлу .c или .cpp. |
| ExclusiveDuration        | * |
| IncludedBy               | Полный путь файла, из которого включается текущий файл. |
| IncludedPath             | Полный путь к текущему файлу. |
| InclusiveDuration        | * |
| InvocationId             | * |
| StartTime                | Метка времени, которая обозначает момент возникновения текущего файлового события. |
| Инструмент                     | * |

\* Этот столбец содержит то же значение, что и в представлении [обозревателя сборки](#build-explorer-view-data-columns).

### <a name="files-view-presets"></a>Предустановки представления файлов

| Имя предустановки | Предпочтительный режим просмотра | Использование |
|-------------|---------------------|------------|
| Статистика  | Таблица               | Вы можете узнать, синтаксический анализ каких файлов занял больше всего суммарного времени, просмотрев список в порядке убывания этого значения. Эта информация поможет вам изменить структуру заголовков или выбрать, что следует включить в предкомпилированный заголовок. |

## <a name="functions"></a>Функции

Представление функций используется для поиска функций, которые создают код в течение очень долгого времени.

### <a name="functions-view-data-columns"></a>Столбцы данных в представлении функций

| Имя столбца              | Описание |
|--------------------------|-------------|
| ActivityName             | Действие, которое выполнялось во время создания текущего события функции. Пока здесь возможно только одно значение: *CodeGeneration*. |
| BuildTimelineDescription | * |
| BuildTimelineId          | * |
| Компонент                | * |
| Count                    | * |
| Duration                 | Длительность действия по созданию кода для этой функции. |
| FunctionName             | Имя функции, для которой выполняется создание кода. |
| InvocationId             | * |
| StartTime                | Отметка времени, которая обозначает момент создания текущего события функции. |
| Инструмент                     | * |

\* Этот столбец содержит то же значение, что и в представлении [обозревателя сборки](#build-explorer-view-data-columns).

### <a name="functions-view-presets"></a>Предустановки представления функций

| Имя предустановки | Предпочтительный режим просмотра | Использование |
|-------------|---------------------|------------|
| Статистика  | Таблица               | Вы можете узнать, создание кода с помощью каких функций занял больше всего суммарного времени, просмотрев список в порядке убывания этого значения. Так вы сможете определить, какие фрагменты кода слишком часто используют ключевое слово **`__forceinline`** или какие функции слишком велики. |
| График выполнения процессов   | График               | Вы можете просмотреть гистограмму, чтобы выяснить расположение и длительность создания функций, на которые потребовалось больше всего времени. Выясните, соответствуют ли они узким местам в представлении обозревателя сборки. Если это так, выполните соответствующие действия для сокращения времени создания кода и оптимизации процесса сборки. |

## <a name="see-also"></a>См. также раздел

[Начало работы с аналитикой сборки C++](../get-started-with-cpp-build-insights.md)\
[Справочник: команды vcperf](vcperf-commands.md)\
[Руководство. Основы использования Windows Performance Analyzer](../tutorials/wpa-basics.md)\
[Windows Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer)

::: moniker-end
