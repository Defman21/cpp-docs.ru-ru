---
description: 'Дополнительные сведения: предупреждение компилятора (уровень 2) C4653'
title: Предупреждение компилятора (уровень 2) C4653
ms.date: 11/04/2016
f1_keywords:
- C4653
helpviewer_keywords:
- C4653
ms.assetid: 90ec3317-3d39-4b4c-bcd1-97e7c799e1b6
ms.openlocfilehash: bf7b2e453d4f9ea90f8b0c187fa834938de15f5a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97173497"
---
# <a name="compiler-warning-level-2-c4653"></a>Предупреждение компилятора (уровень 2) C4653

параметр компилятора "параметр" несовместим с предкомпилированным заголовком; текущий параметр командной строки пропущен

Параметр, указанный в параметре Use предкомпилированные заголовки ([/Yu](../../build/reference/yu-use-precompiled-header-file.md)), не согласуется с параметрами, заданными при создании предкомпилированного заголовка. При компиляции использовался параметр, указанный при создании предкомпилированного заголовка.

Это предупреждение может возникать, если во время компиляции предкомпилированного заголовка было указано другое значение параметра "структуры пакета" ([/Zp](../../build/reference/zp-struct-member-alignment.md)).
