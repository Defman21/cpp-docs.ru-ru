---
description: 'Дополнительные сведения: ошибка сборки проекта PRJ0008'
title: Ошибка построения проекта PRJ0008
ms.date: 11/04/2016
f1_keywords:
- PRJ0008
helpviewer_keywords:
- PRJ0008
ms.assetid: 6bf7f17a-d2a8-4826-99c7-d600d846952f
ms.openlocfilehash: 2ae4952dfd3e5c5f53a3f549536598402ce1fd48
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97343916"
---
# <a name="project-build-error-prj0008"></a>Ошибка построения проекта PRJ0008

Не удалось удалить файл "файл".

**Убедитесь, что файл не открыт другим процессом и не защищен от записи.**

Во время перестроения или очистки Visual C++ удаляет все известные промежуточные и выходные файлы для сборки, а также все файлы, которые соответствуют спецификации шаблона в свойстве " **расширения для удаления** " на [странице свойств Общие параметры конфигурации](../../build/reference/general-property-page-project.md).

Эта ошибка возникает, если Visual C++ не может удалить файл. Чтобы устранить эту ошибку, сделайте файл и его каталог записываемым для пользователя, выполняющего сборку.
