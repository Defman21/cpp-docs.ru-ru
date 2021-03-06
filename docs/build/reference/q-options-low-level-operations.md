---
description: Дополнительные сведения о параметрах/Q (низкоуровневые операции).
title: Параметры /Q (низкоуровневые операции)
ms.date: 01/08/2020
f1_keywords:
- /q
helpviewer_keywords:
- Q compiler option [C++]
- -Q compiler option [C++]
- /Q compiler option [C++]
ms.openlocfilehash: f01781dd670c128f65717a05c6a9367e126550e8
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97225717"
---
# <a name="q-options-low-level-operations"></a>Параметры /Q (низкоуровневые операции)

Параметры компилятора **/q** можно использовать для выполнения следующих низкоуровневых операций компилятора:

- [/Qfast_transcendentals (принудительная Быстрая трансцендентные функции)](qfast-transcendentals-force-fast-transcendentals.md): создает быстрое трансцендентные функции.

- [/QIfist (отключение _ftol)](qifist-suppress-ftol.md): подавляет `_ftol` , если требуется преобразование из типа с плавающей запятой в целочисленный тип (только архитектура x86).

- [/Qimprecise_fwaits (удаление fwaits внутри блоков try)](qimprecise-fwaits-remove-fwaits-inside-try-blocks.md): удаляет `fwait` команды внутри **`try`** блоков.

- [/Кинтел-ЖКК-ерратум](qintel-jcc-erratum.md). снижает влияние на производительность, вызванное обновлением микрокода в условном коде Intel (ЖКК).

- [/Qpar (Auto-параллелизатора)](qpar-auto-parallelizer.md): включает автоматическую параллелизации циклов, которые помечены директивой [цикла #pragma ()](../../preprocessor/loop.md) .

- [/Qpar-report (Auto-Параллелизатора Report Level)](qpar-report-auto-parallelizer-reporting-level.md): включает уровни отчетов для автоматической параллелизации.

- [/Qsafe_fp_loads](qsafe-fp-loads.md): подавляет оптимизацию для загрузок регистров с плавающей запятой и перемещения между регистрами памяти и MMX.

- [/Qspectre](qspectre.md): создает инструкции по устранению некоторых уязвимостей системы безопасности устранением рисков Spectre.

- [/Кспектре-лоад](qspectre-load.md): создает инструкции по устранению уязвимостей безопасности устранением рисков Spectre, основанных на нагрузках.

- [/Кспектре-лоад-КФ](qspectre-load-cf.md): создает инструкции по устранению уязвимостей безопасности устранением рисков Spectre на основе инструкций потока управления, которые загружаются.

- [/Qvec-report (Auto-векторизатора Report Level)](qvec-report-auto-vectorizer-reporting-level.md): включает уровни отчетов для автоматической обработки векторов.

## <a name="see-also"></a>См. также раздел

[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)
