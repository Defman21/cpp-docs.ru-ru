---
description: 'Дополнительные сведения: Добавление элементов в элемент управления "заголовок"'
title: Добавление элементов в элемент управления "Заголовок"
ms.date: 11/04/2016
helpviewer_keywords:
- controls [MFC], header
- CHeaderCtrl class [MFC], adding items
- header controls [MFC], adding items to
ms.assetid: 2e9a28b1-7302-4a93-8037-c5a4183e589a
ms.openlocfilehash: 91c33a7528f6637a91181559d71ed82b13420b38
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97339056"
---
# <a name="adding-items-to-the-header-control"></a>Добавление элементов в элемент управления "Заголовок"

После создания элемента управления "заголовок" ([CHeaderCtrl](reference/cheaderctrl-class.md)) в его родительском окне Добавьте столько элементов заголовка, сколько требуется: обычно по одному на столбец.

### <a name="to-add-a-header-item"></a>Добавление элемента заголовка

1. Подготовьте структуру [HD_ITEM](/windows/win32/api/commctrl/ns-commctrl-hditemw) .

1. Вызовите метод [CHeaderCtrl:: InsertItem](reference/cheaderctrl-class.md#insertitem), передав структуру.

1. Повторите шаги 1 и 2 для дополнительных элементов.

Дополнительные сведения см. в разделе [Добавление элемента в элемент управления "заголовок](/windows/win32/Controls/header-controls) " в Windows SDK.

## <a name="see-also"></a>См. также раздел

[Использование CHeaderCtrl](using-cheaderctrl.md)<br/>
[Элементы управления](controls-mfc.md)
