---
description: 'Дополнительные сведения: активные серверы документов'
title: Серверы активных документов
ms.date: 11/04/2016
helpviewer_keywords:
- active documents [MFC], servers
- servers [MFC], active document
- active document servers [MFC]
ms.assetid: 131fec1e-02a0-4305-a7ab-903b911232a7
ms.openlocfilehash: 37a8e74b0c4b1b37bb031db522bed394c2a9d545
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97150323"
---
# <a name="active-document-servers"></a>Серверы активных документов

Активные серверы документов, такие как Word, Excel или документы размещения PowerPoint для других типов приложений, называемые активными документами. В отличие от внедренных объектов OLE (которые просто отображаются на странице другого документа), активные документы предоставляют полный интерфейс и полные собственные функции серверного приложения, создающего их. Пользователи могут создавать документы, используя все возможности их любимых приложений (если они активны), но могут рассматривать итоговый проект как единую сущность.

Активные документы могут содержать несколько страниц и всегда находятся в активном состоянии. Управление активностью документов в пользовательском интерфейсе путем объединения меню с меню **файл** и **Справка** контейнера. Они занимают всю область редактирования контейнера и управляют представлениями и макетом страницы принтера (поля, нижние колонтитулы и т. д.).

MFC реализует активные серверы документов с помощью интерфейсов документов и представлений, команд диспетчеризации, печати, управления меню и управления реестром. Конкретные требования к программированию обсуждаются в [активных документах](active-documents.md).

MFC поддерживает активные документы с классом [кдокобжектсервер](reference/cdocobjectserver-class.md) , производным от [от CCmdTarget](reference/ccmdtarget-class.md)и [Кдокобжектсерверитем](reference/cdocobjectserveritem-class.md), производным от [COleServerItem](reference/coleserveritem-class.md). MFC поддерживает активные контейнеры документов с классом [COleDocObjectItem](reference/coledocobjectitem-class.md) , производным от [COleClientItem](reference/coleclientitem-class.md).

`CDocObjectServer` сопоставляет интерфейсы активного документа и инициализирует и активирует активный документ. MFC также предоставляет макросы для управления маршрутизацией команд в активных документах. Чтобы использовать активные документы в приложении, включите Афксдокоб. h в файл StdAfx. h.

Обычный сервер MFC подключает собственный `COleServerItem` класс, производный от. Мастер приложений MFC создает этот класс, если установлен флажок **Мини-сервер** или **полный сервер** , чтобы обеспечить поддержку составного документа сервера приложений. Если установить флажок **сервер активных документов** , мастер приложений MFC создаст класс, производный от `CDocObjectServerItem` .

`COleDocObjectItem`Класс позволяет контейнеру OLE стать активным контейнером документа. С помощью мастера приложений MFC можно создать контейнер активного документа, установив флажок **Контейнер активного документа** на странице Поддержка составных документов мастера приложений MFC. Дополнительные сведения см. в разделе [Создание приложения контейнера активного документа](creating-an-active-document-container-application.md).

## <a name="see-also"></a>См. также раздел

[Включение активного документа](active-document-containment.md)
