---
description: 'Дополнительные сведения: идентификаторы ресурсов (символы) (C++)'
title: Идентификаторы ресурсов (символы) (C++)
ms.date: 02/14/2019
f1_keywords:
- vc.editors.symbol.identifiers
helpviewer_keywords:
- symbols [C++], resource identifiers
- symbols [C++], creating
- resource symbols
- symbols [C++], editing
- resource editors [C++], resource symbols
ms.assetid: 8fccc09a-0237-4a65-b9c4-57d60c59e324
ms.openlocfilehash: 1299bb366ba380972d0027dc7285f6ac14dffe37
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97247089"
---
# <a name="resource-identifiers-symbols-c"></a>Идентификаторы ресурсов (символы) (C++)

Символ — это идентификатор ресурса (идентификатор), состоящий из двух частей: имя символа (текстовая строка), сопоставленное со значением символа (целое число), например:

```cpp
IDC_EDITNAME = 5100
```

Под идентификаторами, как правило, подразумевают имена символов.

Символы позволяют описательно ссылаться на ресурсы и объекты пользовательского интерфейса как в исходном коде, так и во время работы с ресурсами в редакторах. Диалоговое окно [Символы ресурсов](./creating-new-symbols.md)представляет собой удобный инструмент, позволяющий выполнять с символами разные действия.

Соответственно тому, как увеличивается размер приложения и сложность его структуры, растет количество ресурсов и символов. Отслеживание большого количества символов, разбросанных по нескольким файлам, может оказаться трудоемкой задачей. Диалоговое окно **символы ресурсов** упрощает управление символами, предоставляя центральное средство, с помощью которого можно:

- [Создание символов](../windows/creating-new-symbols.md)

- [Управление символами](../windows/changing-a-symbol-or-symbol-name-id.md)

- [просмотр предопределенных идентификаторов символов.](../windows/predefined-symbol-ids.md)

В процессе создания ресурса или объекта ресурса [редакторы ресурсов](../windows/resource-editors.md) присваивают ресурсу имя по умолчанию, например `IDC_RADIO1`, а также присваивают ему значение. Определение «имя-плюс-значение» хранится в `Resource.h` файле.

> [!NOTE]
> В процессе копирования ресурсов или объектов ресурсов из одного RC-файла в другой Visual C++ может изменить значение или имя и значение символа копируемого ресурса во избежание конфликтов с именами и значениями символов в существующем файле.

## <a name="requirements"></a>Требования

Win32

## <a name="see-also"></a>См. также раздел

[Работа с файлами ресурсов](../windows/working-with-resource-files.md)<br/>
[Файлы ресурсов](../windows/resource-files-visual-studio.md)<br/>
[Редакторы ресурсов](../windows/resource-editors.md)<br/>
