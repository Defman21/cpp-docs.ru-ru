---
description: 'Дополнительные сведения: Добавление функциональных возможностей в составной элемент управления'
title: Добавление функциональных возможностей в составной элемент управления
ms.date: 11/04/2016
helpviewer_keywords:
- event handlers [C++], ActiveX controls
- composite controls, handling events
- ActiveX controls [C++], events
ms.assetid: 98f85681-9564-480d-af38-03f9733fe58b
ms.openlocfilehash: 90e1f6b0adfc33817f9fa5a6de6fbdcd276241e1
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97166126"
---
# <a name="adding-functionality-to-the-composite-control"></a>Добавление функциональных возможностей в составной элемент управления

После вставки необходимых элементов управления в составной элемент управления следующий шаг включает в себя добавление новых функциональных возможностей. Эти новые функции обычно делятся на две категории:

- Поддержка дополнительных интерфейсов и Настройка поведения составного элемента управления с дополнительными конкретными функциями.

- Обработка событий из содержащегося элемента управления ActiveX (или элементов управления).

Для целей и областей этой статьи оставшаяся часть этого раздела посвящена исключительно обработке событий из элементов управления ActiveX.

> [!NOTE]
> Если необходимо обрабатывать сообщения из элементов управления Windows, см. Дополнительные сведения об обработке сообщений в ATL в разделе [Реализация окна](../atl/implementing-a-window.md) .

После вставки элемента управления ActiveX в ресурс диалогового окна щелкните правой кнопкой мыши элемент управления и выберите команду **Добавить обработчик событий**. Выберите событие, которое необходимо обменять, и нажмите кнопку **Добавить и изменить**. Код обработчика событий будет добавлен в h файл элемента управления.

Точки соединения для элементов управления ActiveX в составном элементе управления автоматически подключаются и отключаются через вызовы [ккомкомпоситеконтрол:: адвисесинкмап](../atl/reference/ccomcompositecontrol-class.md#advisesinkmap).

## <a name="see-also"></a>См. также раздел

[Основные сведения о составном элементе управления](../atl/atl-composite-control-fundamentals.md)
