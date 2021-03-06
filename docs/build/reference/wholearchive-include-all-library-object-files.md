---
description: Дополнительные сведения о:/ВХОЛЕАРЧИВЕ (включение всех файловых объектов библиотеки)
title: /ВХОЛЕАРЧИВЕ (включение всех файлов объектов библиотеки)
ms.date: 02/12/2020
ms.assetid: ee92d12f-18af-4602-9683-d6223be62ac9
ms.openlocfilehash: 1cbc2ad29bab124af90551d2f4a96ee9f08c578c
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97259179"
---
# <a name="wholearchive-include-all-library-object-files"></a>/ВХОЛЕАРЧИВЕ (включение всех файлов объектов библиотеки)

Принудительно включить в компоновщик все объектные файлы в статической библиотеке в связанном исполняемом файле.

## <a name="syntax"></a>Синтаксис

> **/вхолеарчиве**\
> **/Вхолеарчиве:**_Библиотека_

### <a name="arguments"></a>Аргументы

*Библиотечная*\
Необязательный путь к статической библиотеке. Компоновщик включает каждый объектный файл из этой библиотеки.

## <a name="remarks"></a>Комментарии

Параметр/ВХОЛЕАРЧИВЕ заставляет компоновщик включать каждый объектный файл из указанной статической библиотеки или если библиотека не указана, из всех статических библиотек, указанных для команды LINK. Чтобы указать параметр/ВХОЛЕАРЧИВЕ для нескольких библиотек, в командной строке компоновщика можно использовать более одного параметра/ВХОЛЕАРЧИВЕ. По умолчанию компоновщик включает объектные файлы в связанные выходные данные только в том случае, если они экспортируют символы, на которые ссылаются другие файлы объектов в исполняемом файле. Параметр/ВХОЛЕАРЧИВЕ делает компоновщик обрабатывать все объектные файлы, архивированные в статической библиотеке, как если бы они были указаны по отдельности в командной строке компоновщика.

Параметр/ВХОЛЕАРЧИВЕ можно использовать для повторного экспорта всех символов из статической библиотеки. Это позволяет обеспечить включение всего кода библиотеки, ресурсов и метаданных при создании компонента из более чем одной статической библиотеки. Если вы видите предупреждение LNK4264 при создании статической библиотеки, содержащей компоненты среда выполнения Windows для экспорта, используйте параметр/ВХОЛЕАРЧИВЕ при связывании этой библиотеки с другим компонентом или приложением.

Параметр/ВХОЛЕАРЧИВЕ появился в Visual Studio 2015 с обновлением 2.

### <a name="to-set-this-linker-option-in-visual-studio"></a>Настройка этого параметра компоновщика в Visual Studio

1. Откройте диалоговое окно **Окна свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите страницу свойств **Командная строка** в разделе **Свойства конфигурации**, **Компоновщик**.

1. Добавьте параметр/ВХОЛЕАРЧИВЕ в текстовое поле **Дополнительные параметры** .

## <a name="see-also"></a>См. также раздел

[Справочник по компоновщику MSVC](linking.md)<br/>
[Параметры компоновщика MSVC](linker-options.md)
