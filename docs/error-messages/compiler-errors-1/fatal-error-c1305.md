---
description: 'Дополнительные сведения о: Неустранимая ошибка C1305'
title: Неустранимая ошибка C1305
ms.date: 11/04/2016
f1_keywords:
- C1305
helpviewer_keywords:
- C1305
ms.assetid: 1629c850-e2db-4678-83d8-9bfc85323bc5
ms.openlocfilehash: 100046d5ad7c6fa943358063d3d3cb21ffa00e5d
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97267902"
---
# <a name="fatal-error-c1305"></a>Неустранимая ошибка C1305

база данных профиля "pgd_file" предназначена для другой архитектуры

PGD-файл, созданный из операции/LTCG: PGINSTRUMENT для другой платформы, был передан в [/LTCG: PGOPTIMIZE](../../build/reference/ltcg-link-time-code-generation.md) . [Профильная оптимизация](../../build/profile-guided-optimizations.md) доступна для платформ x86 и x64. Однако PGD-файл, созданный с помощью операции/LTCG: PGINSTRUMENT для одной платформы, недопустим в качестве входных данных для файла/LTCG: PGOPTIMIZE для другой платформы.

Чтобы устранить эту ошибку, передайте PGD-файл, созданный с помощью/LTCG: PGINSTRUMENT, в/LTCG: PGOPTIMIZE на той же платформе.
