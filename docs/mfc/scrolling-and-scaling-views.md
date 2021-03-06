---
description: 'Дополнительные сведения: прокрутка и масштабирование представлений'
title: Изменение масштаба и прокрутка представлений
ms.date: 11/04/2016
helpviewer_keywords:
- message handlers [MFC]
- scaling views [MFC]
- message handling [MFC], scroll bars in view class [MFC]
- scroll bars [MFC], messages
- scrolling views [MFC]
ms.assetid: f98a3421-c336-407e-97ee-dbb2ffd76fbd
ms.openlocfilehash: f18b774eadf875f61fcb1f3f3a8dc9e0e370f9a9
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97217813"
---
# <a name="scrolling-and-scaling-views"></a>Изменение масштаба и прокрутка представлений

MFC поддерживает представления для прокрутки и представлений, которые автоматически масштабируются до размера окна фрейма, в котором они отображаются. Класс `CScrollView` поддерживает оба вида представлений.

Дополнительные сведения о прокрутке и масштабировании см. в разделе Class [кскроллвиев](../mfc/reference/cscrollview-class.md) в *справочнике по MFC*. Пример с прокруткой см. в примере [Scribble](../overview/visual-cpp-samples.md).

## <a name="what-do-you-want-to-know-more-about"></a>Что вы хотите узнать подробнее

- Прокрутка представления

- Масштабирование представления

- [Просмотр координат](/windows/win32/gdi/window-coordinate-system)

## <a name="scrolling-a-view"></a><a name="_core_scrolling_a_view"></a> Прокрутка представления

Часто размер документа превышает размер, который может отображаться в его представлении. Это может произойти из-за того, что данные документа увеличиваются или пользователь сжимает окно, которое обработает рамки представления. В таких случаях представление должно поддерживать прокрутку.

Любое представление может выполнять обработку сообщений с полосой прокрутки в своих `OnHScroll` `OnVScroll` функциях-членах и. В этих функциях можно реализовать обработку сообщений с помощью полосы прокрутки, выполнить всю работу самостоятельно или использовать `CScrollView` класс для обработки прокрутки.

Метод `CScrollView` выполняет следующие действия.

- Управляет размерами окон и окна просмотра и режимами сопоставления

- Автоматически прокручивает в ответ на сообщения полосы прокрутки

Можно указать объем прокрутки для "страницы" (когда пользователь щелкает на полосе прокрутки Шафт) и "линия" (когда пользователь щелкает стрелку прокрутки). Спланируйте эти значения в соответствии с характером представления. Например, может потребоваться прокрутка с шагом в 1 пиксель для графического представления, но с приращениями на основе высоты строки в текстовых документах.

## <a name="scaling-a-view"></a><a name="_core_scaling_a_view"></a> Масштабирование представления

Если необходимо, чтобы представление автоматически соответствовало размеру окна фрейма, можно использовать `CScrollView` для масштабирования вместо прокрутки. Логическое представление растягивается или сжимается в точном соответствии с областью окна клиента. Масштабированное представление не имеет полос прокрутки.

## <a name="see-also"></a>См. также раздел

[Использование представлений](../mfc/using-views.md)
