---
description: 'Дополнительные сведения: файлы ресурсов (C++)'
title: Файлы ресурсов (C++)
ms.date: 02/14/2019
f1_keywords:
- vc.editors.resource
helpviewer_keywords:
- resources [C++]
- .rc files [C++]
- resource files [C++]
- resource script files [C++]
- resource script files [C++], Win-32 based applications
- resource script files [C++], files updated when editing resources
- resources [C++], types of resource files
- rct files [C++]
- rc files [C++]
- resource files [C++], types of
- .rct files [C++]
- resource script files [C++], unsupported types
- manifest resources [C++]
- resources [C++], manifest
- resources [C++], opening
- file types [C++], for resources
- resources [C++], editing
- files [C++], editable types
- resource editing
ms.assetid: 4d2b6fcc-07cf-4289-be87-83a60f69533c
ms.openlocfilehash: 8d76a8778cc3c94dd06b6b5b0ea3d6ee6b951e28
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97263327"
---
# <a name="resource-files-c"></a>Файлы ресурсов (C++)

> [!NOTE]
> . Так как в проектах на языках программирования .NET не используются файлы описания ресурсов, ресурсы необходимо открывать из **обозревателя решений**. Используйте [Редактор изображений](../windows/image-editor-for-icons.md) и [двоичный редактор](binary-editor.md) для работы с файлами ресурсов в управляемых проектах.
>
> Все управляемые ресурсы, которые нужно редактировать, должны быть связанными ресурсами. Редакторы ресурсов Visual Studio не поддерживают редактирование внедренных ресурсов.

Термин *файл ресурсов* может ссылаться на несколько типов файлов, например:

- файл описания ресурсов программы (RC);

- файл шаблона ресурсов (RCT);

- Отдельный ресурс, существующий как отдельный файл. Этот тип включает точечный рисунок, значок или файл курсора, на который ссылается RC-файл.

- Файл заголовка, созданный средой разработки. Этот тип включает `Resource.h` , который называется из RC-файла.

Ресурсы, найденные в других типах файлов, таких как exe, DLL и RES-файлы, называются *ресурсами*.

В проекте можно работать с *файлами ресурсов* и *ресурсами* . Вы также можете работать с теми, которые не являются частью текущего проекта или были созданы вне среды разработки Visual Studio. Например, администратор может сделать следующее:

- Работать с вложенными и условно включенными файлами ресурсов.

- Обновите существующие ресурсы или преобразуйте их в Visual C++.

- Импортировать графические ресурсы в текущий файл ресурсов или экспортировать их из него.

- Включать общие или доступные только для чтения идентификаторы (символы), которые нельзя изменить с помощью среды разработки.

- Включите ресурсы в исполняемый файл (exe), который не нуждается в редактировании (или не следует изменять), например общие ресурсы между несколькими проектами.

- Включать типы ресурсов, не поддерживаемые средой разработки.

Дополнительные сведения о ресурсах см. в статьях [Создание ресурсов](../windows/how-to-create-a-resource-script-file.md), [Управление ресурсами](../windows/how-to-copy-resources.md)и [Включение ресурсов во время компиляции](../windows/how-to-include-resources-at-compile-time.md).

## <a name="editable-resources"></a>Изменяемые ресурсы

Чтобы изменить содержащиеся в них ресурсы, можно открыть следующие типы файлов:

| Имя файла | Описание |
|---|---|
| .rc | Файлы скриптов ресурсов |
| .rct | Файлы шаблонов ресурсов |
| RES | Файлы ресурсов |
| .resx | Управляемые файлы ресурсов |
| EXE | Исполняемые файлы |
| DLL | Файлы библиотек динамической компоновки |
| . bmp,. ico,. DIB,. cur | Точечные рисунки, значки, панели инструментов и файлы курсоров |

При редактировании ресурсов среда Visual Studio работает с и влияет на следующие файлы:

| Имя файла | Описание |
|---|---|
| Resource.h | Файл заголовка, созданный средой разработки, которая содержит определения символов.<br/><br/>Включить этот файл в систему управления версиями. |
| Filename.aps | Двоичная версия текущего файла скрипта ресурсов, используемая для быстрой загрузки.<br /><br /> Редакторы ресурсов не читают файлы RC или resource. h напрямую. Компилятор ресурсов компилирует их в APS файлы, используемые редакторами ресурсов. Этот файл представляет собой этап компиляции и содержит только символьные данные.<br/><br/>Как и в случае обычного процесса компиляции, сведения, не являющиеся символьными, например комментарии, удаляются во время компиляции.<br/><br/>Если файл APS не синхронизирован с RC-файлом, RC-файл создается повторно. Например, при **сохранении** редактор ресурсов перезаписывает файл. RC и файл Resource. h. Любые изменения в ресурсах остаются включенными в RC-файл, но при перезаписании RC-файла комментарии всегда будут потеряны. Сведения о том, как сохранять комментарии, см. в разделе [Включение ресурсов во время компиляции](../windows/how-to-include-resources-at-compile-time.md).<br/><br/>Как правило, файл APS не должен включаться в систему управления версиями. |
| .rc | Файл описания ресурсов, содержащий скрипт для ресурсов в текущем проекте. Этот файл перезаписывается APS-файлом при каждом сохранении.<br/><br/>Включить этот файл в систему управления версиями. |

## <a name="manifest-resources"></a>Ресурсы манифеста

В проектах классических приложений C++ Ресурсы манифеста представляют собой XML-файлы, описывающие зависимости, используемые приложением. Например, в Visual Studio созданный мастером MFC файл манифеста определяет, какую версию библиотек DLL общих элементов управления Windows должно использовать приложение:

```xml
<description>Your app description here</description>
<dependency>
    <dependentAssembly>
        <assemblyIdentity
            type="win32"
            name="Microsoft.Windows.Common-Controls"
            version="6.0.0.0"
            processorArchitecture="X86"
            publicKeyToken="6595b64144ccf1df"
            language="*"
        />
    </dependentAssembly>
</dependency>
```

Для приложения Windows XP или Windows Vista ресурс манифеста должен указывать последнюю версию стандартных элементов управления Windows для использования приложением. В приведенном выше примере используется версия `6.0.0.0` , которая поддерживает [элемент управления Syslink](/windows/win32/Controls/syslink-overview).

> [!NOTE]
> Допускается иметь только один ресурс манифеста на каждый модуль.

Чтобы просмотреть сведения о версии и типе, содержащиеся в ресурсе манифеста, откройте файл в средстве просмотра XML-данных или в текстовом редакторе Visual Studio. Если вы откроете ресурс манифеста из [представления ресурсов](./how-to-create-a-resource-script-file.md), этот ресурс откроется в двоичном формате.

### <a name="to-open-a-manifest-resource"></a>Открытие ресурса манифеста

1. Откройте проект в Visual Studio и перейдите к **Обозреватель решений**.

1. Разверните папку **файлы ресурсов** , а затем:

   - Чтобы открыть его в текстовом редакторе, дважды щелкните файл *. manifest* .

   - Чтобы открыть в другом редакторе, щелкните правой кнопкой мыши файл *manifest* и выберите команду **Открыть с помощью**. Укажите используемый редактор и нажмите кнопку **Открыть**.

## <a name="requirements"></a>Требования

Win32

## <a name="see-also"></a>См. также раздел

[Работа с файлами ресурсов](../windows/working-with-resource-files.md)<br/>
[Идентификаторы ресурсов (символы)](../windows/symbols-resource-identifiers.md)<br/>
[Редакторы ресурсов](../windows/resource-editors.md)<br/>
