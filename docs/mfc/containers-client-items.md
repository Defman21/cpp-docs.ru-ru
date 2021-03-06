---
description: 'Дополнительные сведения: контейнеры: клиентские элементы'
title: Контейнеры. Элементы клиентов
ms.date: 11/04/2016
helpviewer_keywords:
- OLE containers [MFC], client items
- client items and OLE containers
ms.assetid: 231528b5-0744-4f83-8897-083bf55ed087
ms.openlocfilehash: e8aff84e825723b1615a0dbbadf7d5fec6d4cef1
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97310438"
---
# <a name="containers-client-items"></a>Контейнеры. Элементы клиентов

В этой статье объясняется, что такое элементы клиента и какие классы приложение должно наследовать от своих клиентских элементов.

Клиентские элементы — это элементы данных, принадлежащие другому приложению, которые либо содержатся в документе приложения контейнера OLE, либо ссылаются на него. Клиентские элементы, данные которых содержатся в документе, внедряются; данные, которые хранятся в другом расположении, на которое ссылается документ-контейнер, связаны.

Класс документа в приложении OLE является производным от класса [коледокумент](reference/coledocument-class.md) , а не от `CDocument` . `COleDocument`Класс наследует от `CDocument` всех функций, необходимых для использования архитектуры "документ-представление", на которой основаны приложения MFC. `COleDocument` также определяет интерфейс, который обрабатывает документ как коллекцию `CDocItem` объектов. `COleDocument`Для добавления, извлечения и удаления элементов этой коллекции предусмотрено несколько функций элементов.

Каждое приложение контейнера должно наследовать хотя бы один класс от `COleClientItem` . Объекты этого класса представляют элементы, внедренные или связанные, в документе OLE. Эти объекты существуют в течение жизненного цикла документа, содержащего их, если только они не удалены из документа.

`CDocItem` является базовым классом для `COleClientItem` и `COleServerItem` . Объекты классов, производных от этих двух, действуют как посредники между элементом OLE и клиентскими и серверными приложениями соответственно. Каждый раз, когда в документ добавляется новый элемент OLE, платформа MFC добавляет новый объект `COleClientItem` производного клиентского приложения в коллекцию `CDocItem` объектов документа.

## <a name="see-also"></a>См. также раздел

[Контейнеры](containers.md)<br/>
[Контейнеры: составные файлы](containers-compound-files.md)<br/>
[Контейнеры: проблемы User-Interface](containers-user-interface-issues.md)<br/>
[Контейнеры: дополнительные функции](containers-advanced-features.md)<br/>
[Класс COleClientItem](reference/coleclientitem-class.md)<br/>
[Класс COleServerItem](reference/coleserveritem-class.md)
