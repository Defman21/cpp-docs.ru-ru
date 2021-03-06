---
description: Дополнительные сведения о:/PROFILE (профилировщик средств оценки производительности)
title: /PROFILE (профилировщик средств обеспечения производительности)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCLinkerTool.Profile
helpviewer_keywords:
- -PROFILE linker option
- /PROFILE linker option
ms.assetid: e676baa1-5063-47a3-a357-ba0d1f0d1699
ms.openlocfilehash: fb9310bb782a4b321113155f01db2228e3a46e15
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97225795"
---
# <a name="profile-performance-tools-profiler"></a>/PROFILE (профилировщик средств обеспечения производительности)

Создает выходной файл, который может быть использован для профилировщика производительности инструментов.

## <a name="syntax"></a>Синтаксис

```
/PROFILE
```

## <a name="remarks"></a>Remarks

/PROFILE подразумевает следующие параметры компоновщика:

- [/OPT: REF](opt-optimizations.md)

- /OPT: NOICF

- [/INCREMENTAL: НЕТ](incremental-link-incrementally.md)

- [/FIXED: НЕТ](fixed-fixed-base-address.md)

/PROFILE заставляет компоновщик создать раздел перемещения в образе программы.  Раздел перемещения позволяет профилировщику преобразовать образ программы для получения данных профиля.

**/Profile** доступен только в версиях Enterprise (коллективная разработка).  Дополнительные сведения о экспресс-анализе см. в разделе [анализ кода для C/C++ обзор](../../code-quality/code-analysis-for-c-cpp-overview.md).

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Задание данного параметра компоновщика в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Разверните узел **Свойства конфигурации**.

1. Разверните узел **Компоновщик**.

1. Выберите страницу свойств **Дополнительно**.

1. Измените свойство **Profile** .

### <a name="to-set-this-linker-option-programmatically"></a>Задание данного параметра компоновщика программным способом

1. См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.Profile%2A>.

### <a name="to-set-this-linker-option-within-visual-studio-cmake-project"></a>Установка этого параметра компоновщика в проекте CMak в Visual Studio

В проекте **CMAK** нет **страниц свойств**, параметры компоновщика можно задать, Интернете CMakeLists.txt.

1. Откройте CMakeLists.txt в корневом каталоге проекта.

1. Добавьте код ниже. Дополнительные сведения см. в разделе [Справочники по CMAK](https://cmake.org/cmake/help/v3.0/command/set_target_properties.html) .

1. Перестройте решение.

```
SET_TARGET_PROPERTIES(${PROJECT_NAME} PROPERTIES LINK_FLAGS "/PROFILE")
```

## <a name="see-also"></a>См. также:

[Справочник по компоновщику MSVC](linking.md)<br/>
[Параметры компоновщика MSVC](linker-options.md)
