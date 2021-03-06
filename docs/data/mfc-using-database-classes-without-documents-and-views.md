---
description: 'Дополнительные сведения: MFC: использование классов базы данных без документов и представлений'
title: MFC. Использование классов базы данных без документов и представлений
ms.date: 11/04/2016
helpviewer_keywords:
- ODBC applications [C++], without views
- documents [C++], applications without
- ODBC applications [C++]
- document/view architecture [C++], in databases
- files [C++], MFC
- database classes [C++], MFC
- CRecordView class, using in database applications
- database applications [C++], without views
- database applications [C++], application wizard options
- application wizards [C++], creating database applications
- ODBC [C++], file support in database applications
- ODBC applications [C++], without documents
- database applications [C++], without documents
- user interface [C++], drawing information
ms.assetid: 15bf52d4-91cf-4b1d-8b37-87c3ae70123a
ms.openlocfilehash: 32b019286a07cacc0c7bf95145d0aedde804ff92
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97295163"
---
# <a name="mfc-using-database-classes-without-documents-and-views"></a>MFC. Использование классов базы данных без документов и представлений

Иногда вам может не понадобиться использовать архитектуру документов и представлений платформы в приложениях базы данных. В этом разделе рассматриваются следующие вопросы.

- [Если нет необходимости использовать такие документы](#_core_when_you_don.92.t_need_documents) , как сериализация документов.

- [Параметры мастера приложений](#_core_appwizard_options_for_documents_and_views) для поддержки приложений без сериализации и **без связанных с** документом команд меню « **создать**», « **Открыть**», « **сохранить**» и **«Сохранить как**».

- [Как работать с приложением, использующим минимальный документ](#_core_applications_with_minimal_documents).

- [Как структурировать приложение без документа или представления](#_core_applications_with_no_document).

## <a name="when-you-do-not-need-documents"></a><a name="_core_when_you_don.92.t_need_documents"></a> Если документы не нужны

Некоторые приложения имеют отдельную концепцию документа. Эти приложения обычно загружают все или большинство файлов из хранилища в память с помощью команды **открытия файла** . Они записывают обновленный файл обратно в хранилище всего за один раз с помощью команды **сохранить файл** или **Сохранить как** . Пользователь видит файл данных.

Однако для некоторых категорий приложений не требуется документ. Приложения базы данных работают с точки зрения транзакций. Приложение выбирает записи из базы данных и предоставляет их пользователю, как правило, по одной за раз. То, что видит пользователь, обычно является одной текущей записью, которая может быть единственной в памяти.

Если приложению не требуется документ для хранения данных, вы можете рассветить некоторые или все архитектуру документа или представления платформы. Объем, с которым вы можете распределяться, зависит от предпочтительного подхода. Вы можете:

- Используйте минимальный документ в качестве места для сохранения подключения к источнику данных, но с помощью обычных функций документа, таких как сериализация. Это полезно, если требуется несколько представлений данных и требуется синхронизировать все представления, одновременно обновляя все эти данные и т. д.

- Используйте окно фрейма, в котором можно нарисовать непосредственно, а не использовать представление. В этом случае вы не пропускаете документ и сохраняете данные или подключения к данным в объекте фреймового окна.

## <a name="application-wizard-options-for-documents-and-views"></a><a name="_core_appwizard_options_for_documents_and_views"></a> Параметры мастера приложений для документов и представлений

В мастере приложений MFC имеется несколько параметров в окне **Поддержка базы данных**, которые перечислены в следующей таблице. При использовании мастера приложений MFC для создания приложения все эти параметры создают приложения с документами и представлениями. Некоторые параметры предоставляют документы и представления, не пропуская ненужные функции документов. Дополнительные сведения см. в разделе [Поддержка баз данных, мастер приложений MFC](../mfc/reference/database-support-mfc-application-wizard.md).

|Параметр|Представление|Документ|
|------------|----------|--------------|
|**Нет**|Производное от `CView`.|Не поддерживает базу данных. Это параметр по умолчанию.<br /><br /> При выборе параметра **Поддержка архитектуры документов/представлений** на странице [Тип приложения, мастер приложений MFC](../mfc/reference/application-type-mfc-application-wizard.md) вы получаете полную поддержку документов, включая сериализацию, а также команды **создать**, **Открыть**, **сохранить** и **Сохранить как** в меню **файл** . См. раздел [приложения без документа](#_core_applications_with_no_document).|
|**Только файлы заголовков**|Производное от `CView`.|Предоставляет базовый уровень поддержки баз данных для вашего приложения.<br /><br /> Включает Афксдб. h. Добавляет библиотеки ссылок, но не создает классы, относящиеся к базе данных. Вы можете создавать наборы записей позже и использовать их для проверки и обновления записей.|
|**Представление базы данных без поддержки файлов**|Производный от `CRecordView`|Предоставляет поддержку документов, но не поддерживает сериализацию. Документ может хранить набор записей и координировать несколько представлений. не поддерживает сериализацию или команды " **создать**", " **Открыть**", " **сохранить**" и " **Сохранить как** ". См. раздел [приложения с минимальными документами](#_core_applications_with_minimal_documents). При включении представления базы данных необходимо указать источник данных.<br /><br /> Включает файлы заголовков базы данных, библиотеки компоновки, представление записей и набор записей. (Доступно только для приложений с **поддержкой архитектуры "документ/представление** ", выбранной на странице [мастера приложений MFC](../mfc/reference/application-type-mfc-application-wizard.md) .)|
|**Представление базы данных с поддержкой файлов**|Производный от `CRecordView`|Обеспечивает полную поддержку документов, включая сериализацию и команды меню **файл** , связанные с документом. Приложения баз данных обычно работают с каждой записью, а не с каждым файлом и поэтому не требуют сериализации. Однако для сериализации может использоваться специальное предложение. См. раздел [приложения с минимальными документами](#_core_applications_with_minimal_documents). При включении представления базы данных необходимо указать источник данных.<br /><br /> Включает файлы заголовков базы данных, библиотеки компоновки, представление записей и набор записей. (Доступно только для приложений с **поддержкой архитектуры "документ/представление** ", выбранной на странице [мастера приложений MFC](../mfc/reference/application-type-mfc-application-wizard.md) .)|

Описание альтернатив для сериализации и альтернативных вариантов использования сериализации см. в разделе [сериализация: сериализация и ввод-вывод базы данных](../mfc/serialization-serialization-vs-database-input-output.md).

## <a name="applications-with-minimal-documents"></a><a name="_core_applications_with_minimal_documents"></a> Приложения с минимальными документами

Мастер приложений MFC поддерживает два варианта поддержки приложений для доступа к данным на основе форм. Каждый параметр создает `CRecordView` производный класс представления и документ. Они отличаются тем, что они оставляют за пределами документа.

### <a name="document-without-file-support"></a><a name="_core_a_document_without_file_support"></a> Документ без поддержки файлов

Выберите параметр базы данных мастер приложений **представление базы данных без поддержки файлов** , если не требуется сериализация документов. Документ служит для следующих полезных целей:

- Это удобное место для хранения `CRecordset` объекта.

   Это использование параллельно с обычными концепциями документа: документ хранит данные (или, в данном случае, набор записей), а представление — представление документа.

- Если приложение представляет несколько представлений (например, несколько представлений записей), документ поддерживает координацию представлений.

   Если несколько представлений отображают одни и те же данные, можно использовать `CDocument::UpdateAllViews` функцию члена для координации обновлений во всех представлениях при изменении данных в любом представлении.

Этот параметр обычно используется для простых приложений на основе форм. Мастер приложений автоматически поддерживает для таких приложений удобную структуру.

### <a name="document-with-file-support"></a><a name="_core_a_document_with_file_support"></a> Документ с поддержкой файлов

Выберите параметр базы данных мастер приложений **представление базы данных с поддержкой файлов** при наличии альтернативного использования команд меню **файл** , связанных с документом, и сериализации документов. Для части программы доступа к данным можно использовать документ так же, как описано в [документе без поддержки файлов](#_core_a_document_without_file_support). Можно использовать возможность сериализации документа, например, для чтения и записи документа сериализованного профиля пользователя, в котором хранятся предпочтения пользователя или другие полезные сведения. Дополнительные идеи см. в разделе [сериализация: сериализация и ввод-вывод базы данных](../mfc/serialization-serialization-vs-database-input-output.md).

Мастер приложений поддерживает этот параметр, но необходимо написать код, который сериализует документ. Хранение сериализованной информации в элементах данных документа.

## <a name="applications-with-no-document"></a><a name="_core_applications_with_no_document"></a> Приложения без документов

Иногда может потребоваться написать приложение, которое не использует документы или представления. Без документов данные (например, `CRecordset` объект) хранятся в классе окна фрейма или в классе приложения. Дополнительные требования зависят от того, представляет ли приложение пользовательский интерфейс.

### <a name="database-support-with-a-user-interface"></a><a name="_core_database_support_with_a_user_interface"></a> Поддержка баз данных с помощью пользовательского интерфейса

Если у вас есть пользовательский интерфейс (отличный от, например, интерфейс командной строки консоли), приложение будет непосредственно работать в клиентской области окна фрейма, а не в представлении. Такое приложение не использует `CRecordView` , `CFormView` или `CDialog` для основного пользовательского интерфейса, но обычно используется `CDialog` для обычных диалоговых окон.

### <a name="writing-applications-without-documents"></a><a name="_core_writing_applications_without_documents"></a> Написание приложений без документов

Поскольку мастер приложений не поддерживает создание приложений без документов, необходимо написать собственный `CWinApp` класс, производный от, и при необходимости создать `CFrameWnd` `CMDIFrameWnd` класс или. Переопределите `CWinApp::InitInstance` и объявите объект приложения как:

```cpp
CYourNameApp theApp;
```

Платформа по-прежнему предоставляет механизм карт сообщений и многие другие функции.

### <a name="database-support-separate-from-the-user-interface"></a><a name="_core_database_support_separate_from_the_user_interface"></a> Поддержка баз данных, отделенная от пользовательского интерфейса

Некоторым приложениям не требуется пользовательский интерфейс или минимум один. Например, предположим, что вы пишете:

- Промежуточный объект доступа к данным, который вызывается другими приложениями (клиентами) для специальной обработки данных между приложением и источником данных.

- Приложение, обрабатывающее данные без вмешательства пользователя, например приложение, которое перемещает данные из одного формата базы данных в другой или в одну из них, выполняющую вычисления и выполнение пакетных обновлений.

Так как ни один из документов не владеет `CRecordset` объектом, вероятно, вы захотите сохранить его как внедренный элемент данных в `CWinApp` классе производного приложения. Ниже представлены возможные альтернативы.

- Не постоянное хранение постоянного `CRecordset` объекта. В конструкторы класса набора записей можно передать значение NULL. В этом случае платформа создает временный объект, `CDatabase`  используя сведения в `GetDefaultConnect` функции-члене набора записей. Это наиболее вероятный альтернативный подход.

- Назначение `CRecordset` объекту глобальной переменной. Эта переменная должна быть указателем на объект набора записей, который вы динамически создаете в `CWinApp::InitInstance` переопределении. Это позволяет избежать попытки создать объект перед инициализацией платформы.

- Использование объектов Recordset как в контексте документа или представления. Создание наборов записей в функциях-членах объектов приложения или окна фрейма.

## <a name="see-also"></a>См. также раздел

[Классы баз данных MFC](../data/mfc-database-classes-odbc-and-dao.md)
