---
description: 'Дополнительные сведения: варианты проектирования приложений'
title: Решения, которые необходимо принять при разработке приложения
ms.date: 09/12/2019
helpviewer_keywords:
- design
- application design [MFC], design goals
- application design [MFC], Internet applications
- Internet applications [MFC], designing applications
- Internet [MFC], vs. intranets
- applications [MFC], Internet
- server applications [MFC], vs. client applications on Internet
- client applications [MFC], vs. server applications on Internet
ms.assetid: 9b96172c-b4d4-4c69-bfb2-226ce0de6d08
ms.openlocfilehash: 0402cfe8cb58ed538e1429d2edc4f95cc9a23a0c
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97335924"
---
# <a name="application-design-choices"></a>Решения, которые необходимо принять при разработке приложения

В этой статье рассматриваются некоторые проблемы проектирования, которые следует учитывать при программировании для Интернета.

В этой статье рассматриваются следующие темы:

- [Интрасеть и Интернет](#_core_intranet_versus_internet)

- [Клиентское или серверное приложение](#_core_client_or_server_application)

- [Веб-страница](#_core_the_web_page)

- [Браузер или приложение Stand-Alone](#_core_browser_or_standalone)

- [COM в Интернете](#_core_com_on_the_internet)

- [Службы загрузки данных клиента](#_core_client_data_download_services)

Если вы готовы начать писать программу прямо сейчас, см. статью [написание приложений MFC](writing-mfc-applications.md).

## <a name="intranet-versus-internet"></a><a name="_core_intranet_versus_internet"></a> Интрасеть и Интернет

Многие приложения работают в Интернете и доступны любому пользователю с браузером и доступом в Интернет. Компании также реализуют интрасети, которые являются корпоративными сетями, использующими протоколы TCP/IP и веб-браузеры. Интрасети предлагают легко обновляемый, центральный источник информации для всей Организации. Они могут использоваться для обновления программного обеспечения, для доставки опросов, поддержки клиентов и доставки информации. В следующей таблице сравниваются функции Интернета и интрасетей.

|Интернет|Интрасеть|
|--------------|--------------|
|Низкая пропускная способность|Высокая пропускная способность|
|Сниженная безопасность данных и систем|Контролируемый доступ к данным и системам|
|Минимальный контроль над содержимым|Высокий уровень контроля над содержимым|

## <a name="client-or-server-application"></a><a name="_core_client_or_server_application"></a> Клиентское или серверное приложение

Приложение может выполняться на клиентском компьютере или на компьютере сервера. Приложение также может храниться на сервере, а затем загружаться через Интернет и запускать на клиентском компьютере. Классы MFC WinInet используются для загрузки файлов клиентскими приложениями. Классы MFC и асинхронных классов моникера используются для загрузки файлов и свойств элементов управления. Классы для элементов ActiveX и активные документы используются для клиентских приложений и для приложений, загружаемых с сервера для запуска на клиенте.

## <a name="the-web-page-html-active-documents-activex-controls"></a><a name="_core_the_web_page"></a> Веб-страница: HTML, активные документы, элементы управления ActiveX

Корпорация Майкрософт предлагает несколько способов предоставления содержимого на веб-странице. Веб-страницы могут использовать стандартные расширения HTML или HTML, такие как тег объекта, для предоставления динамического содержимого, такого как элементы управления ActiveX.

В веб-браузерах обычно отображаются HTML-страницы. Активные документы также могут отображать данные приложения в простом интерфейсе "точка — щелчок" в браузере с поддержкой COM. Сервер активных документов может отображать документ, полный кадр во всей клиентской области с собственными меню и панелями инструментов.

Записываемые элементы ActiveX можно загружать асинхронно с сервера и отображать на веб-странице. С помощью языка сценариев, такого как VBScript, можно выполнить проверку на стороне клиента перед отправкой данных на сервер.

## <a name="browser-or-stand-alone-application"></a><a name="_core_browser_or_standalone"></a> Браузер или приложение Stand-Alone

Элементы управления ActiveX, внедренные в HTML-страницу и активные серверы документов, просматриваемые в браузере, можно создавать. Можно создать HTML-страницы, содержащие кнопку для отправки запроса на запуск приложения ISAPI на веб-сервере. Вы можете написать автономное приложение, использующее протоколы Интернета для загрузки файлов и вывода их пользователю без использования приложения браузера.

## <a name="com-on-the-internet"></a><a name="_core_com_on_the_internet"></a> COM в Интернете

Все элементы управления ActiveX, активные документы и асинхронные моникеры используют технологии COM (объектной модели компонентов).

Элементы управления ActiveX предоставляют динамическое содержимое для документов и страниц на веб-сайтах. С помощью модели COM можно создавать элементы управления ActiveX и полнофункциональные документы, используя активные документы.

Асинхронные моникеры предоставляют функции, позволяющие элементу управления работать в среде Интернета, включая добавочные или прогрессивные средства для загрузки данных. Кроме того, элементы управления должны хорошо работать с другими элементами управления, которые также могут получать данные асинхронно в одно и то же время.

## <a name="client-data-download-services"></a><a name="_core_client_data_download_services"></a> Службы загрузки данных клиента

Два набора API, которые помогут передавать данные клиенту, — это WinInet и асинхронные моникеры. Если на странице HTML имеются большие GIF-и AVI-файлы и элементы управления ActiveX, можно увеличить скорость реагирования для пользователя, загрузив асинхронно, либо с помощью асинхронных моникеров, либо с помощью WinInet в асинхронном режиме.

Распространенная задача в Интернете — передача данных. Если вы уже используете активную технологию (например, если у вас есть элемент управления ActiveX), можно использовать асинхронные моникеры для поэтапного отображения данных во время загрузки. Вы можете использовать WinInet для перемещения данных с помощью общих Интернет-протоколов, таких как HTTP, FTP и gopher. Оба метода обеспечивают независимость от протокола и предоставляют абстрактный уровень для использования WinSock и TCP/IP. Вы по-прежнему можете использовать [Winsock](windows-sockets-in-mfc.md) напрямую.

В следующей таблице приведены несколько способов использования MFC для перемещения данных через Интернет.

|Использовать этот протокол|В этих условиях|Использование этих классов|
|-----------------------|----------------------------|-------------------------|
|[Загрузка через Интернет с использованием асинхронных моникеров](asynchronous-monikers-on-the-internet.md)|Для асинхронной пересылки с использованием COM, элементов управления ActiveX и любого протокола Интернета.|[Касинкмоникерфиле](reference/casyncmonikerfile-class.md), [кдатапаспроперти](reference/cdatapathproperty-class.md)|
|[WinInet](win32-internet-extensions-wininet.md)|Для протоколов Интернета для HTTP, FTP и gopher. Данные могут передаваться синхронно или асинхронно и храниться в кэше на уровне системы.|[Цинтернетсессион](reference/cinternetsession-class.md), [кфтпфилефинд](reference/cftpfilefind-class.md), [кгоферфилефинд](reference/cgopherfilefind-class.md)и многие другие.|
|[WinSock](windows-sockets-in-mfc.md)|Для достижения максимальной эффективности и контроля. Требует понимания сокетов и протоколов TCP/IP.|[CSocket](reference/csocket-class.md), [CAsyncSocket](reference/casyncsocket-class.md)|

## <a name="see-also"></a>См. также раздел

[Задачи программирования в Интернете MFC](mfc-internet-programming-tasks.md)<br/>
[Основные сведения о программировании Интернета MFC](mfc-internet-programming-basics.md)<br/>
[Расширения Интернета Win32 (WinInet)](win32-internet-extensions-wininet.md)<br/>
[Асинхронные моникеры в Интернете](asynchronous-monikers-on-the-internet.md)
