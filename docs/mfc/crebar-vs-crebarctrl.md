---
description: 'Дополнительные сведения о: Кребар и CReBarCtrl'
title: CReBar или CReBarCtrl
ms.date: 11/04/2016
helpviewer_keywords:
- CReBar class [MFC], vs. CReBarCtrl
- rebar controls [MFC], CReBarCtrl class [MFC]
- GetReBarCtrl class [MFC]
ms.assetid: 7f9c1d7e-5d5f-4956-843c-69ed3df688d0
ms.openlocfilehash: 5a8dfe7594448319b4eb872abfb7022841d4e5dd
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97309437"
---
# <a name="crebar-vs-crebarctrl"></a>CReBar или CReBarCtrl

MFC предоставляет два класса для создания ребарс: [кребар](reference/crebar-class.md) и [CReBarCtrl](reference/crebarctrl-class.md) (который заключает в оболочку общий API элемента управления Windows). `CReBar` предоставляет все функциональные возможности общего элемента управления "Главная панель" и обрабатывает многие из необходимых общих параметров и структур элементов управления.

`CReBarCtrl` является классом-оболочкой для элемента управления главной панели Win32 и, следовательно, может быть проще в реализации, если не планируется интегрировать главную панель в архитектуру MFC. Если вы планируете использовать `CReBarCtrl` и интегрировать главную панель в архитектуру MFC, необходимо принять дополнительные меры для передачи управления главной панелью в MFC. Это несложная связь. Однако это дополнительная работа, которая не требуется при использовании `CReBar` .

Visual C++ предоставляет два способа использования преимуществ общего элемента управления "Главная панель".

- Создайте главную панель с помощью `CReBar` , а затем вызовите [кребар:: жетребарктрл](reference/crebar-class.md#getrebarctrl) , чтобы получить доступ к `CReBarCtrl` функциям элементов.

    > [!NOTE]
    >  `CReBar::GetReBarCtrl` — Это встроенная функция-член, которая приводит **`this`** указатель объекта главной панели. Это означает, что во время выполнения вызов функции не имеет издержек.

- Создание главной панели с помощью конструктора [CReBarCtrl](reference/crebarctrl-class.md).

Любой из методов предоставит доступ к функциям элементов элемента управления "Главная панель". При вызове `CReBar::GetReBarCtrl` он возвращает ссылку на `CReBarCtrl` объект, чтобы можно было использовать любой набор функций-членов. Сведения о создании и создании главной панели с помощью см. в разделе [кребар](reference/crebar-class.md) `CReBar` .

## <a name="see-also"></a>См. также раздел

[Использование CReBarCtrl](using-crebarctrl.md)<br/>
[Элементы управления](controls-mfc.md)
