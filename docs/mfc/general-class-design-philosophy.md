---
description: 'Дополнительные сведения: общие принципы проектирования классов'
title: Общие принципы разработки классов
ms.date: 11/04/2016
helpviewer_keywords:
- designing classes [MFC]
- MFC, Windows API
- Visual C, Windows API calls
- classes [MFC], MFC class design
- Windows API [MFC], and MFC
ms.assetid: e6861ae0-1581-4d9c-9ddf-63f9afcdb913
ms.openlocfilehash: 96069b5f30cbca8bb310de6b917fd65a280700b0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97193465"
---
# <a name="general-class-design-philosophy"></a>Общие принципы разработки классов

Microsoft Windows была разработана долго, прежде чем язык C++ стал популярным. Поскольку тысячи приложений используют программный интерфейс Windows (API) для языка C, этот интерфейс будет поддерживаться в ожидаемом будущем. Следовательно, любой интерфейс C++ должен быть создан на основе процедурного API языка C. Это гарантирует, что приложения C++ смогут сосуществовать с приложениями C.

Библиотека Microsoft Foundation Class представляет собой объектно-ориентированный интерфейс для Windows, который соответствует следующим целям проектирования:

- Значительное сокращение усилий на написание приложения для Windows.

- Скорость выполнения, сравнимая с интерфейсом API языка C.

- Минимальный размер кода.

- Возможность непосредственного вызова любой функции Windows C.

- Упрощенное преобразование существующих приложений C в C++.

- Возможность использовать существующую основу интерфейса программирования Windows на языке C.

- Упрощенное использование API Windows с C++, чем с C.

- Более удобные и удобные в использовании мощные абстракции сложных функций, таких как элементы управления ActiveX, поддержка баз данных, печать, панели инструментов и строки состояния.

- Настоящий API Windows для C++, который эффективно использует возможности языка C++.

Дополнительные сведения о проектировании библиотеки MFC см. в следующих статьях:

- [Платформа приложений](application-framework.md)

- [Связь с API языка C](relationship-to-the-c-language-api.md)

## <a name="see-also"></a>См. также раздел

[Общие сведения о классах](class-library-overview.md)
