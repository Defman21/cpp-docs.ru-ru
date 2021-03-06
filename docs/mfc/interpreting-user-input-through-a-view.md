---
description: Дополнительные сведения см. в статье анализ вводимых пользователем данных с помощью представления.
title: Интерпретация ввода пользователя через представление
ms.date: 11/04/2016
helpviewer_keywords:
- interpreting user input through views [MFC]
- views [MFC], user interface and input
- input [MFC], view class [MFC]
- CView class [MFC], interpreting user input
- user input [MFC], interpreting through view class [MFC]
ms.assetid: f0302a70-661f-4781-8fe7-78f082bef2a5
ms.openlocfilehash: f3442a13bc60b7424840e23673806c1e5120c4ad
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97335841"
---
# <a name="interpreting-user-input-through-a-view"></a>Интерпретация ввода пользователя через представление

Другие функции элементов обработчика представления и интерпретации всех вводимых пользователем данных. Как правило, в классе представления для обработки можно определить функции-члены обработчика сообщений:

- [Сообщения](messages.md) Windows, создаваемые действиями мыши и клавиатуры.

- [Команды](user-interface-objects-and-command-ids.md) из меню, кнопок панели инструментов и сочетаний клавиш.

Эти функции-члены обработчика сообщений преобразуют следующие действия в качестве входных данных, выбора или редактирования, включая перемещение данных в буфер обмена и из него:

- Перемещение по щелчку мыши, перетаскивание и двойные щелчки

- Нажатий клавиш

- Команды меню

Сообщения Windows, обрабатываемые дескрипторами представления, зависят от потребностей вашего приложения.

В [разделах обработка и сопоставление сообщений](message-handling-and-mapping.md) объясняется, как назначить пункты меню и другие объекты пользовательского интерфейса командам и как привязать команды к функциям обработчика. В [разделах обработка и сопоставление сообщений](message-handling-and-mapping.md) также объясняется, как MFC маршрутизирует команды и отправляет стандартные сообщения Windows объектам, содержащим обработчики для них.

Например, приложению может потребоваться реализовать прямую прорисовку мыши в представлении. В образце Scribble показано, как управлять сообщениями WM_LBUTTONDOWN, WM_MOUSEMOVE и WM_LBUTTONUP соответственно, чтобы начать, продолжить и завершить рисование сегмента линии. С другой стороны, иногда может потребоваться интерпретировать щелчок мыши в представлении в качестве выделения. `OnLButtonDown`Функция обработчика вашего представления определит, была ли пользователь изображена или выбрана. Если выбрать, обработчик определит, находится ли щелчок в границах некоторого объекта в представлении, и, если это так, изменить отображение, чтобы показать объект как выбранный.

Представление может также работать с определенными командами меню, например из меню Правка для вырезания, копирования, вставки или удаления выбранных данных с помощью буфера обмена. Такой обработчик вызовет некоторые функции-члены класса, связанные с буфером обмена, `CWnd` для перемещения выбранного элемента данных в буфер обмена или из него.

## <a name="see-also"></a>См. также раздел

[Использование представлений](using-views.md)
