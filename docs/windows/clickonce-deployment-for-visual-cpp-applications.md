---
description: 'Дополнительные сведения: развертывание ClickOnce для приложений Visual C++'
title: Развертывание с помощью технологии ClickOnce для приложений Visual C++
ms.date: 11/04/2016
helpviewer_keywords:
- deploying applications [C++], ClickOnce
- application deployment [C++], ClickOnce
- ClickOnce deployment [C++], C++ applications
ms.assetid: 9988c546-0936-452c-932f-9c76daa42157
ms.openlocfilehash: eb888e9236eec16ba82c82c11a23428163679e97
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97118216"
---
# <a name="clickonce-deployment-for-visual-c-applications"></a>Развертывание с помощью технологии ClickOnce для приложений Visual C++

Visual Studio предоставляет две различных технологии развертывания приложений Windows: ClickOnce и [установщик Windows](/windows/win32/Msi/windows-installer-portal).

## <a name="clickonce-deployment-in-c"></a>Развертывание с помощью технологии ClickOnce в C++

Среда разработки Visual C++ не поддерживает развертывание проектов Visual Studio C++ с помощью ClickOnce напрямую, но для его использования доступны средства.

> [!NOTE]
> Visual Studio поддерживает ClickOnce в средах развертывания Visual C# и Visual Basic. Если проект Visual Studio C++ является зависимостью проекта Visual C#, можно опубликовать приложение (включая его зависимости) с помощью развертывания ClickOnce из среды разработки Visual C#.

Для развертывания приложения Visual C++ с помощью ClickOnce сначала нужно создать [Манифест приложения ClickOnce](/visualstudio/deployment/clickonce-application-manifest) и [Манифест развертывания ClickOnce](/visualstudio/deployment/clickonce-deployment-manifest) с помощью [Mage.exe](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool) (Инструмент создания и изменения манифестов) или его версий для графического пользовательского интерфейса (сведения см. в разделе [MageUI.exe (средство создания и редактирования манифестов, графический клиент)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)).

Используя Mage.exe, создайте манифест приложения; полученный файл будет иметь расширение MANIFEST. Затем с помощью Mage.exe создайте манифест развертывания; полученный файл будет иметь расширение APPLICATION. Теперь необходимо подписать манифесты.

В манифесте приложения должен быть указан целевой процессор (**x86**, **x64** или **ARM**). Сведения об этих вариантах см. в разделе [Предварительные условия для развертывания 64-разрядных приложений](/visualstudio/deployment/deploying-prerequisites-for-64-bit-applications).

Кроме этого, имена манифестов приложения и развертывания не должны совпадать с именем приложения С++. Это позволит избежать конфликта между манифестом приложения, созданным с помощью Mage.exe, и внешним манифестом, являющимся частью приложения C++.

При развертывании должны быть установлены все библиотеки Visual C++, от которых зависит работа приложения. Чтобы определить зависимости для конкретного приложения, можно воспользоваться файлом depends.exe или служебной программой DUMPBIN, запустив ее с параметром /DEPENDENTS. Дополнительные сведения о зависимостях см. в разделе [Основные сведения о зависимостях приложения Visual C++](understanding-the-dependencies-of-a-visual-cpp-application.md). Может возникнуть потребность в выполнении VCRedist.exe; эта служебная программа устанавливает библиотеки Visual C++ на конечный компьютер.

Может также потребоваться создать начальный загрузчик (установщик необходимых компонентов) для приложения, чтобы развернуть необходимые компоненты. Подробнее о начальном загрузчике см. в разделе [Создание пакетов загрузчика](/visualstudio/deployment/creating-bootstrapper-packages).

Подробные сведения об этой технологии представлены в разделе [Развертывание и безопасность технологии ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment). Подробный пример развертывания ClickOnce см. в разделе [Пошаговое руководство. Развертывание вручную приложения ClickOnce](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application).

## <a name="see-also"></a>См. также раздел

[Mage.exe (средство создания и редактирования манифеста)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)<br>
[MageUI.exe (средство создания и редактирования манифестов, графический клиент)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)<br>
[Makecert.exe (средство создания сертификатов)](/windows/win32/SecCrypto/makecert)<br>
[Развертывание классических приложений](deploying-native-desktop-applications-visual-cpp.md)<br>
[Развертывание приложений, служб и компонентов](/visualstudio/deployment/deploying-applications-services-and-components)<br>
[Развертывание и безопасность технологии ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment)<br>
[Создание пакетов загрузчика](/visualstudio/deployment/creating-bootstrapper-packages)<br>
[Программирование .NET с использованием C++/CLI (Visual C++)](../dotnet/dotnet-programming-with-cpp-cli-visual-cpp.md)<br>
[Взаимодействие машинного кода и .NET](../dotnet/native-and-dotnet-interoperability.md)
