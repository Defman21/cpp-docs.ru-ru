---
description: 'Дополнительные сведения: создание немодальных диалоговых окон'
title: Создание немодальных диалоговых окон
ms.date: 11/04/2016
helpviewer_keywords:
- MFC dialog boxes [MFC], modeless
- modeless dialog boxes [MFC], creating
- MFC dialog boxes [MFC], creating
ms.assetid: 70d78c7f-3d40-477b-9f78-0f33c359f88b
ms.openlocfilehash: c754391a0f1ab2713f3ce01b5d30ccc33be4aaa5
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97309788"
---
# <a name="creating-modeless-dialog-boxes"></a>Создание немодальных диалоговых окон

Для немодального диалогового окна необходимо предоставить собственный открытый конструктор в классе диалогового окна. Чтобы создать немодальное диалоговое окно, вызовите открытый конструктор, а затем вызовите функцию-член [создания](reference/cdialog-class.md#create) объекта диалогового окна, чтобы загрузить ресурс диалогового окна. Можно вызвать метод **CREATE** либо во время, либо после вызова конструктора. Если в ресурсе диалога имеется свойство **WS_VISIBLE**, диалоговое окно отображается немедленно. В противном случае необходимо вызвать свою функцию члена [ShowWindow](reference/cwnd-class.md#showwindow) .

## <a name="see-also"></a>См. также раздел

[Работа с диалоговыми окнами в MFC](life-cycle-of-a-dialog-box.md)
