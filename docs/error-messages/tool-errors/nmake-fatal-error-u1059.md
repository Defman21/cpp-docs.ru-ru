---
description: 'Дополнительные сведения: Неустранимая ошибка NMAKE U1059'
title: Неустранимая ошибка NMAKE U1059
ms.date: 08/27/2018
f1_keywords:
- U1059
helpviewer_keywords:
- U1059
ms.assetid: b21d9198-9c63-40d0-b589-80e17294ce24
ms.openlocfilehash: 025ea8577814519b883e534c54ed8cf4383ef029
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97283541"
---
# <a name="nmake-fatal-error-u1059"></a>Неустранимая ошибка NMAKE U1059

> Синтаксическая ошибка: "}" отсутствует в зависимости

Неправильно указан путь поиска для зависимого элемента. Пропускается либо пробел в пути, либо закрывающая фигурная скобка (**}**).

Синтаксис спецификации каталога для зависимых объектов

> зависят от **{** *Directories* **}**

*Каталог* WHERE указывает один или несколько путей, разделенных точкой с запятой (**;**). Пробелы не допускаются.

Если часть или полный путь поиска заменяется макросом, убедитесь, что в расширении макроса не существует пробелов.
