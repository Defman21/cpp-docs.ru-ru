---
title: Структура TRACE_INFO_DATA
description: Справочник по структуре TRACE_INFO_DATA из пакета SDK для Аналитики сборок C++.
ms.date: 02/12/2020
helpviewer_keywords:
- C++ Build Insights
- C++ Build Insights SDK
- TRACE_INFO_DATA
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: ce6301b168aed9f279fc7aaee9aa3a97221fd23a
ms.sourcegitcommit: 9c2b3df9b837879cd17932ae9f61cdd142078260
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "92923422"
---
# <a name="trace_info_data-structure"></a>Структура TRACE_INFO_DATA

::: moniker range="<=msvc-140"

Пакет SDK Аналитики сборок С++ совместим с Visual Studio 2017 и более поздних версий. Чтобы увидеть документацию для этих версий, установите в данной статье селектор **Версия** Visual Studio в Visual Studio 2017 или Visual Studio 2019. Он находится в верхней части оглавления на этой странице.

::: moniker-end
::: moniker range=">=msvc-150"

В структуре `TRACE_INFO_DATA` описывается анализируемая и повторно записываемая трассировка.

## <a name="syntax"></a>Синтаксис

```cpp
typedef struct TRACE_INFO_DATA_TAG
{
    unsigned long           LogicalProcessorCount;
    long long               TickFrequency;
    long long               StartTimestamp;
    long long               StopTimestamp;

} TRACE_INFO_DATA;
```

## <a name="members"></a>Участники

| Имя | Описание |
|--|--|
| `LogicalProcessorCount` | Количество логических процессоров на компьютере, на котором производилась трассировка. |
| `TickFrequency` | Количество тактов в секунду, которое используется при оценке длительности, изменяемой в тактах. |
| `StartTimestamp` | В этом поле сохраняется значение тактов, захваченное в момент запуска действия. |
| `StopTimestamp` | В этом поле сохраняется значение тактов, захваченное в момент остановки действия. |

## <a name="remarks"></a>Remarks

Вычтите `StartTimestamp` из `StopTimestamp`, чтобы получить число тактов, прошедших во время всей трассировки. Используйте `TickFrequency`, чтобы преобразовать полученное значение в единицу времени. Пример преобразования тактов в единицы времени см. в статье о [EVENT_DATA](event-data-struct.md).

::: moniker-end
