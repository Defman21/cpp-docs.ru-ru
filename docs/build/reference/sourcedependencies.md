---
title: /sourceDependencies (отчет о зависимостях на уровне источника)
description: Справочное руководство по параметру компилятора/СаурцедепенденЦиес в Microsoft C++.
ms.date: 07/29/2020
f1_keywords:
- /sourceDependencies
helpviewer_keywords:
- /sourceDependencies compiler option
- /sourceDependencies
ms.openlocfilehash: 0c1866812435c777f6f1fd7ed7f9db788a8cf031
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2020
ms.locfileid: "91502838"
---
# <a name="sourcedependencies-report-source-level-dependencies"></a>`/sourceDependencies` (Отчеты о зависимостях на уровне источника)

Указывает компилятору создать JSON-файл, который содержит подробные сведения о зависимостях на уровне источника, потребляемых во время компиляции.

JSON-файл содержит список исходных зависимостей, включая следующие:

- Файлы заголовков (как транзитивные, так и непосредственно включаемые заголовки).
- Используемый PCH (если **`/Yu`** указан).
- Импортированные модули и импортированные единицы заголовков (транзитивные и непосредственно импортированные модули и единицы заголовка).

## <a name="syntax"></a>Синтаксис

> **`/sourceDependencies`***имя файла*\
> **`/sourceDependencies`***Каталог*

## <a name="arguments"></a>Аргументы

*файлов*\
Компилятор записывает выходные данные исходной зависимости в указанное имя файла, которое может включать относительный или абсолютный путь.

*каталоги*\
Если аргумент является каталогом, компилятор создает исходные файлы зависимостей в указанном каталоге. Имя выходного файла основано на полном имени входного файла с добавленным *`.json`* расширением. Например, если файл, предоставленный компилятору, имеет значение *`main.cpp`* , то созданное выходное имя файла будет равно *`main.cpp.json`* .

## <a name="remarks"></a>Remarks

**`/sourceDependencies`** Параметр компилятора доступен начиная с Visual Studio 2019 версии 16,7. По умолчанию оно отключено.

При указании **`/MP`** параметра компилятора рекомендуется использовать **`/sourceDependencies`** с аргументом каталога. Если указать один аргумент имени файла, два экземпляра компилятора могут попытаться открыть выходной файл одновременно и вызвать ошибку. Дополнительные сведения о **`/MP`** см. в разделе [ `/MP` (сборка с несколькими процессами)](mp-build-with-multiple-processes.md).

При возникновении неустранимой ошибки компилятора сведения о зависимостях по-прежнему записываются в выходной файл.

Все пути к файлам отображаются в выходных данных в виде абсолютных путей.

### <a name="examples"></a>Примеры

С учетом следующего примера кода:

```cpp
// main.cpp
#include "header.h"
import m;
import "other.h";

int main() { }
```

Вы можете использовать **`/sourceDependencies`** вместе с остальными параметрами компилятора:

> `cl ... /sourceDependencies output.json ... main.cpp`

где `...` представляет другие параметры компилятора. Эта командная строка создает JSON *`output.json`* -файл с содержимым примерно следующего вида:

```JSON
{
    "Version": "1.0",
    "Data": {
        "Source": "C:\\...\\main.cpp",
        "PCH": "C:\\...\\pch.pch",
        "Includes": [
            "C:\\...\\header.h"
        ],
        "Modules": [
            "C:\\...\\m.ifc",
            "C:\\...\\other.h.ifc"
        ]
    }
}
```

Мы использовали `...` для сокращения путей к отчетам; отчет содержит абсолютные пути. Полученные пути зависят от того, где компилятор находит зависимости. Если результаты являются непредвиденными, может потребоваться проверить параметры пути включения проекта.

### <a name="to-set-the-sourcedependencies-compiler-option-in-visual-studio"></a>Установка параметра компилятора/СаурцедепенденЦиес в Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите страницу свойств **Свойства конфигурации**  >  **C/C++**  >  **Командная строка** .

1. В поле **Дополнительные параметры** добавьте, *`/sourceDependencies: <filename>`* а затем нажмите кнопку **ОК** или **Применить** , чтобы сохранить изменения.

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- Этот параметр не имеет программного эквивалента.

## <a name="see-also"></a>См. также раздел

[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис командной строки компилятора MSVC](compiler-command-line-syntax.md)<br/>
