---
description: Дополнительные сведения о том, что такое объект CArchive
title: Понятие объекта CArchive
ms.date: 11/04/2016
helpviewer_keywords:
- archive objects [MFC]
- archives [MFC], for serialization
- buffers, serializable objects
- CArchive class [MFC], about CArchive class [MFC]
- buffering, serializable objects
ms.assetid: 843f1825-288d-4d89-a1fa-70e1f92d9b8b
ms.openlocfilehash: 7d98200f87f4b428a9450894aca5f8958115d627
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97142796"
---
# <a name="what-is-a-carchive-object"></a>Понятие объекта CArchive

`CArchive`Объект предоставляет механизм буферизации с поддержкой строгой типизации для записи или чтения сериализуемых объектов в объект или из него `CFile` . Обычно `CFile` объект представляет дисковый файл, однако он также может быть файлом памяти ( `CSharedFile` объектом), возможно представляющим буфер обмена.

Данный `CArchive` объект либо сохраняет (записывает, сериализует) данные, либо загружает (считывает, десериализует) данные, но никогда не оба. Срок жизни `CArchive` объекта ограничен одним проходом по записи объектов в файл или чтением объектов из файла. Таким словами, `CArchive` для сериализации данных в файл и последующей десериализации их из файла необходимо создать два последовательных объекта.

Когда архив сохраняет объекты в файл, Архив прикрепляет `CRuntimeClass` имя к объектам. Затем, когда другой архив загружает объекты из файла в память, `CObject` производные объекты динамически перестроятся на основе `CRuntimeClass` объектов. На данный объект можно ссылаться более одного раза, так как он записывается в файл при хранении архива. Однако загрузка архива приведет к реконструированию объекта только один раз. Сведения о том, как Архив присоединяет `CRuntimeClass` сведения к объектам и реконструирует объекты, принимая во внимание возможные многочисленные ссылки, описаны в технической статье [2](../mfc/tn002-persistent-object-data-format.md).

По мере сериализации данных в архив этот архив накапливает данные до заполнения буфера. Затем Архив записывает свой буфер в `CFile` объект, на который указывает `CArchive` объект. Аналогично, при чтении данных из архива он считывает данные из файла в буфер, а затем из буфера в десериализованный объект. Такая буферизация сокращает число физических операций чтения жесткого диска, тем самым повышая производительность приложения.

## <a name="see-also"></a>См. также раздел

[Сериализация: сериализация объекта](../mfc/serialization-serializing-an-object.md)
