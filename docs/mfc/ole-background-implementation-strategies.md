---
description: 'Дополнительные сведения о: OLE Background: стратегии реализации'
title: Поддержка OLE. Стратегии реализации
ms.date: 11/04/2016
helpviewer_keywords:
- OLE [MFC], development strategy
- OLE applications [MFC], implementing OLE
- applications [OLE], implementing OLE
ms.assetid: 0875ddae-99df-488c-82c6-164074a81058
ms.openlocfilehash: fe492adf755f9163586832f5c7aa7dfc5470349f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97275481"
---
# <a name="ole-background-implementation-strategies"></a>Поддержка OLE. Стратегии реализации

В зависимости от приложения существует четыре возможные стратегии реализации поддержки OLE:

- Вы пишете новое приложение.

   Эта ситуация обычно требует наименьшей работы. Чтобы создать скелет приложения, запустите мастер приложений MFC и выберите пункт Дополнительные функции или поддержка составных документов. Сведения об этих параметрах и их возможностях см. в статье [Создание программы MFC exe](reference/mfc-application-wizard.md).

- У вас есть программа, написанная с библиотека Microsoft Foundation Class версии 2,0 или более поздней, которая не поддерживает OLE.

   Создайте новое приложение с помощью мастера приложений MFC, как упоминалось ранее, а затем скопируйте и вставьте код из нового приложения в существующее приложение. Это будет работать для серверов, контейнеров или автоматических приложений. Пример этой стратегии см. в примере MFC [Scribble](../overview/visual-cpp-samples.md) .

- Имеется программа библиотека Microsoft Foundation Class, которая реализует поддержку OLE версии 1,0.

   Эта стратегия преобразования представлена в [техническом примечании MFC 41](tn041-mfc-ole1-migration-to-mfc-ole-2.md) .

- У вас есть приложение, которое не было написано с помощью Microsoft Foundation Classes и может не реализовать поддержку OLE.

   Эта ситуация требует наибольшей работы. Одним из подходов является создание нового приложения, как в первой стратегии, а затем копирование и вставка существующего кода в него. Если существующий код написан на языке C, может потребоваться изменить его, чтобы он мог компилироваться как код C++. Если код на языке C вызывает API Windows, нет необходимости изменять его для использования классов Microsoft Foundation. Этот подход, скорее всего, потребует некоторой реструктуризации программы для поддержки архитектуры "документ-представление", используемой в версиях 2,0 и более поздних Microsoft Foundation Classes. Дополнительные сведения об этой архитектуре см. в [техническом примечании 25](tn025-document-view-and-frame-creation.md).

После принятия решения по стратегии следует прочесть статьи о [контейнерах](containers.md) или [серверах](servers.md) (в зависимости от типа приложения, который вы пишете) или изучить примеры программ или и то, и другое. Примеры MFC OLE [OCLIENT](../overview/visual-cpp-samples.md) и [HIERSVR](../overview/visual-cpp-samples.md) показывают, как реализовать различные аспекты контейнеров и серверов соответственно. В различных местах в этих статьях вы будете называть определенные функции в этих примерах как примеры обсуждаемых методик.

## <a name="see-also"></a>См. также раздел

[Фон OLE](ole-background.md)<br/>
[Контейнеры: Реализация контейнера](containers-implementing-a-container.md)<br/>
[Серверы: реализация сервера](servers-implementing-a-server.md)<br/>
[Мастер приложений MFC](reference/mfc-application-wizard.md)
