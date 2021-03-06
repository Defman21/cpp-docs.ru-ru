---
description: 'Дополнительные сведения: обработка кнопки "Применить"'
title: Обработка кнопки "Применить"
ms.date: 11/04/2016
helpviewer_keywords:
- Apply button in property sheet
- property sheets, Apply button
ms.assetid: 7e977015-59b8-406f-b545-aad0bfd8d55b
ms.openlocfilehash: a626dcab04d68d19efba79465bfca46545ff6670
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97254941"
---
# <a name="handling-the-apply-button"></a>Обработка кнопки "Применить"

Вкладки свойств имеют возможность не использовать стандартные диалоговые окна: они позволяют пользователю применять сделанные ими изменения перед закрытием страницы свойств. Это делается с помощью кнопки Применить. В этой статье обсуждаются методы, которые можно использовать для правильной реализации этой функции.

Модальные диалоговые окна обычно применяют параметры к внешнему объекту, когда пользователь нажимает кнопку ОК, чтобы закрыть диалоговое окно. Это справедливо и для страницы свойств: когда пользователь нажимает кнопку ОК, новые параметры на странице свойств вступают в силу.

Однако может потребоваться разрешить пользователю сохранять параметры без закрытия диалогового окна «Страница свойств». Это функция кнопки Применить. Кнопка применить применяет текущие параметры ко всем страницам свойств к внешнему объекту, в отличие от применения текущих параметров активной страницы.

По умолчанию кнопка применить всегда отключена. Необходимо написать код, чтобы включить кнопку применить в нужное время, и необходимо написать код для реализации результата применения, как описано ниже.

Если вы не хотите предоставлять пользователю функцию Apply, нет необходимости удалять кнопку Применить. Вы можете оставить его отключенным, как будет общим для приложений, использующих стандартную поддержку страниц свойств, доступных в будущих версиях Windows.

Чтобы сообщить странице об изменении и включить кнопку Применить, вызовите `CPropertyPage::SetModified( TRUE )` . Если какой-либо из страниц отчета изменяется, кнопка применить остается включенной независимо от того, была ли изменена текущая активная страница.

Метод [CPropertyPage:: SetModified](reference/cpropertypage-class.md#setmodified) следует вызывать каждый раз, когда пользователь изменяет какие-либо параметры на странице. Одним из способов определить, когда пользователь изменяет параметр на странице, является реализация обработчиков уведомлений об изменениях для каждого элемента управления на странице свойств, например **EN_CHANGE** или **BN_CLICKED**.

Чтобы применить действие кнопки Применить, страница свойств должна сообщить владельцу или другому внешнему объекту в приложении о применении текущих параметров на страницах свойств. В то же время на странице свойств следует отключить кнопку Применить, вызвав `CPropertyPage::SetModified( FALSE )` для всех страниц, которые применяют свои изменения к внешнему объекту.

Пример этого процесса см. в общем примере MFC [пропдлг](../overview/visual-cpp-samples.md).

## <a name="see-also"></a>См. также раздел

[Вкладки свойств](property-sheets-mfc.md)
