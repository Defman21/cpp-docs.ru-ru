---
description: 'Дополнительные сведения: предупреждение компилятора (уровень 1) C4729'
title: Предупреждение компилятора (уровень 1) C4729
ms.date: 11/04/2016
f1_keywords:
- C4729
helpviewer_keywords:
- C4729
ms.assetid: 36a0151f-f258-48d9-9444-ae6d41ff70a4
ms.openlocfilehash: de4da8a56f4b8c6788b972a154e8670c14c07d68
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97272218"
---
# <a name="compiler-warning-level-1-c4729"></a>Предупреждение компилятора (уровень 1) C4729

Слишком большая функция для предупреждений, основанных на графе потока выполнения

Это предупреждение возникает в случае, если функция слишком велика для компиляции с надежной проверкой ситуаций, в которых могут возникать предупреждения. Это предупреждение появляется только в том случае, если используется параметр компилятора [/Od](../../build/reference/od-disable-debug.md) .

Чтобы устранить это предупреждение, разделите функцию на более мелкие функции.
