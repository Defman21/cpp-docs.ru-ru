---
description: 'Дополнительные сведения о: параметром/USEPROFILE (запуск профильной оптимизации в потокобезопасный режим)'
title: ПАРАМЕТРОМ/USEPROFILE (использование данных профильной оптимизации с LTCG)
ms.date: 03/14/2018
f1_keywords:
- USEPROFILE
ms.openlocfilehash: c6c293b8467ea308dc2f7b4a4cd916cc5d9ac4c9
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97247050"
---
# <a name="useprofile-run-pgo-in-thread-safe-mode"></a>ПАРАМЕТРОМ/USEPROFILE (запуск PGO в защищенном режиме потока)

Этот параметр компоновщика вместе с [/LTCG (создание кода во время компоновки](ltcg-link-time-code-generation.md) ) указывает компоновщику выполнить сборку с помощью обучающих данных по профильной оптимизации (PGO).

## <a name="syntax"></a>Синтаксис

> **Параметром/useprofile**[**:**{**агрессивная** | **PGD =**_filename_}]

### <a name="arguments"></a>Аргументы

**Активная**<br/>
Этот необязательный аргумент указывает, что для создания оптимизированного кода следует использовать агрессивную оптимизацию скорости.

**PGD** = *имя файла*<br/>
Указывает имя базового файла для PGD-файла. По умолчанию компоновщик использует базовое имя исполняемого файла с расширением PGD.

## <a name="remarks"></a>Комментарии

Параметр компоновщика **параметром/useprofile** используется вместе с **/LTCG** для создания или обновления оптимизированной сборки на основе данных для обучения профильной оптимизации. Это эквивалентно нерекомендуемым параметрам **/LTCG: PGUPDATE** и **/LTCG: PGOPTIMIZE** .

Необязательный аргумент **агрессивно** отключает эвристику, связанную с размером, для оптимизации скорости. Это может привести к оптимизации, которые значительно увеличивают размер исполняемого файла и могут не увеличить полученную скорость. Следует пропрофилировать и сравнить результаты использования и не использовать **агрессивные**. Этот аргумент должен быть указан явным образом. по умолчанию оно отключено.

Аргумент **PGD** указывает необязательное имя для используемого файла обучающих данных. pgd, то же, что и в [/GENPROFILE или/FASTGENPROFILE](genprofile-fastgenprofile-generate-profiling-instrumented-build.md). Это эквивалент параметра нерекомендуемого параметра **/PGD** . По умолчанию или если *имя файла* не указано, используется PGD-файл с тем же базовым именем, что и у исполняемого файла.

Параметр компоновщика **параметром/useprofile** впервые используется в Visual Studio 2015.

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>Задание данного параметра компоновщика в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите   >    >  страницу свойств **Оптимизация** компоновщика свойств конфигурации.

1. В свойстве **время создания кода времени компоновки** выберите **использовать создание кода во время компоновки (/LTCG)**.

1. Перейдите на страницу свойств **Свойства конфигурации** > **Компоновщик** > **Командная строка**.

1. В поле **Дополнительные параметры** введите параметр **параметром/useprofile** и необязательные аргументы. Выберите **ОК** для сохранения внесенных изменений.

### <a name="to-set-this-linker-option-programmatically"></a>Задание данного параметра компоновщика программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>См. также раздел

[/GENPROFILE и /FASTGENPROFILE](genprofile-fastgenprofile-generate-profiling-instrumented-build.md)<br/>
[Указан](ltcg-link-time-code-generation.md)<br/>
[Профильная оптимизация](../profile-guided-optimizations.md)<br/>
[Переменные среды для оптимизации Profile-Guided](../environment-variables-for-profile-guided-optimizations.md)<br/>
