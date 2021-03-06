---
description: Подробнее о pgomgr
title: pgomgr
ms.date: 03/14/2018
helpviewer_keywords:
- pgomgr program
- profile-guided optimizations, pgomgr
ms.assetid: 74589126-df18-42c9-8739-26d60e148d6a
ms.openlocfilehash: 3b6b969becde43b98ea06f2058dd235eaf0acbed
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97187355"
---
# <a name="pgomgr"></a>pgomgr

Добавляет данные профиля из одного или нескольких PGC в файл PGD.

## <a name="syntax"></a>Синтаксис

> **pgomgr** [*options*] *pgcfiles* *pgdfile*

### <a name="parameters"></a>Параметры

*options*<br/>
Можно указать следующие параметры для **pgomgr**:

- **/help** или **/?** . Вывод доступных параметров **pgomgr**.

- **/clear**. Удаление всех сведений профиля из файла PGD. Если указан параметр **/clear**, указать файл PGC невозможно.

- **/detail**. Вывод подробной статистики, включая сведения о покрытии графа потока.

- **/summary**. Вывод статистики по функциям.

- **/unique**. При использовании совместно с параметром **/summary** выводятся дополненные имена функций. По умолчанию, если параметр **/unique** не используется, имена функций отображаются без дополнений.

- **/merge**\[ **:** <em>n</em>]. Добавление данных из одного или нескольких файлов PGC в файл PGD. Необязательный параметр, *n*, позволяет указать, что данные должны добавляться *n* раз. Например, если сценарий обычно выполняется в шесть раз, чтобы отразить, как часто они выполняются клиентами, можно сделать это один раз в тестовом запуске и добавить его в файл PGD шесть раз с помощью команды **pgomgr /merge: 6**.

*pgcfiles*.<br/>
Один или несколько файлов PGC, данные профиля в которых необходимо объединить в один файл PGD. Можно указать один файл PGC или несколько файлов PGC. Если файлы PGC не указаны, **pgomgr** объединяет все файлы PGC, имена которых совпадают с файлом PGD.

*pgdfile*.<br/>
Файл PGD, в который объединяются данные из одного или нескольких файлов PGC.

## <a name="remarks"></a>Примечания

> [!NOTE]
> Это средство можно запустить только из командной строки разработчика Visual Studio. В системной командной строке или проводнике это невозможно.

## <a name="example"></a>Пример

Ниже приведен пример команды, которая удаляет данные профиля из файла myapp.pgd:

`pgomgr /clear myapp.pgd`

Ниже приведен пример команды, которая добавляет данные профиля из файла myapp1.pgc в файл PGD три раза:

`pgomgr /merge:3 myapp1.pgc myapp.pgd`

В этом примере данные профиля из всех файлов myapp#.pgc добавляются в файл myapp.pgd.

`pgomgr -merge myapp1.pgd`

## <a name="see-also"></a>См. также

[Профильная оптимизация](profile-guided-optimizations.md)<br/>
[PgoAutoSweep](pgoautosweep.md)<br/>
[pgosweep](pgosweep.md)<br/>
