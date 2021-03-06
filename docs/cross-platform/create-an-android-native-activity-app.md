---
description: 'Дополнительные сведения: создание приложения Android Native Activity'
title: Создание приложения Android Native Activity
ms.date: 10/17/2019
ms.assetid: 884014b1-5208-45ec-b0da-ad0070d2c24d
ms.openlocfilehash: d8ccccde40c89553d12fd98645cda2877e581273
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97319330"
---
# <a name="create-an-android-native-activity-app"></a>Создание приложения Android Native Activity

После установки кроссплатформенной рабочей нагрузки **Разработка мобильных приложений на языке C++** Visual Studio можно использовать для создания полнофункциональных приложений Android Native Activity. Пакет Android Native Development Kit (NDK) — это набор средств, с помощью которых можно реализовывать большинство возможностей приложения Android, используя чистый код C или C++. Для обеспечения взаимодействия кода C или C++ с Android используется определенный код Java JNI, выступающий в роли связующего. В Android NDK появилась возможность создавать приложения Native Activity с помощью API Android уровня 9. Код Native Activity популярен для создания игровых приложений и приложений с интенсивным использованием графики на основе Unreal Engine или OpenGL. В этом пошаговом руководстве показано создание простого приложения Native Activity, в котором используется OpenGL. В дополнительных разделах последовательно рассматриваются такие этапы жизненного цикла разработки, как редактирование, сборка, отладка и развертывание кода Native Activity.

## <a name="requirements"></a>Требования

Прежде чем создавать приложение Android Native Activity, необходимо убедиться, что вы выполнили все системные требования и установили рабочую нагрузку **Разработка мобильных приложений на языке C++** в Visual Studio. Дополнительные сведения см. в статье [Установка Visual C++ для разработки кроссплатформенных мобильных приложений на языке C++](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md). Убедитесь, что необходимые сторонние инструменты и пакеты SDK включены в установку, а также что установлен эмулятор Android.

## <a name="create-a-new-native-activity-project"></a>Создание проекта Native Activity

В этом руководстве вы сначала создадите новый проект Android Native Activity, а затем создадите и запустите приложение по умолчанию в эмуляторе Android.

::: moniker range="msvc-150"

1. В Visual Studio выберите **Файл** > **Создать** > **Проект**.

1. В диалоговом окне **Новый проект** в меню **Шаблоны** последовательно выберите **Visual C++** > **Кроссплатформенное приложение**, а затем выберите шаблон **Приложение Native-Activity (Android)**.

1. Присвойте приложению имя, например *MyAndroidApp*, а затем нажмите **OK**.

   ![Создание проекта Native Activity](../cross-platform/media/cppmdd-newproject.png "Создание проекта Native Activity")

   Visual Studio создаст новое решение и откроет обозреватель решений.

   ![Проект Native Activity в обозревателе решений](../cross-platform/media/cppmdd-rc-na-solutionexp.png "Проект Native Activity в Solution Explorer")

::: moniker-end

::: moniker range=">=msvc-160"

1. В Visual Studio выберите **Файл** > **Создать** > **Проект**.

1. В диалоговом окне **Создание нового проекта** выберите шаблон **Приложение Native-Activity (Android)**, а затем нажмите **Далее**.

1. В диалоговом окне **Настроить новый проект** введите имя, например *MyAndroidApp* в разделе **Имя проекта**, а затем выберите **Создать**.

   Visual Studio создаст новое решение и откроет обозреватель решений.

::: moniker-end

В новое решение приложения Android Native Activity входят два проекта.

- `MyAndroidApp.NativeActivity` содержит ссылки и связующий код для запуска приложения как приложения Native Activity на Android. Реализация точек входа из связывающего кода находится в *Main. cpp*. Предкомпилированные заголовки находятся в *PCH. h*. Этот проект приложения с собственным действием компилируется в общую библиотеку *.* файл, который забирается проектом упаковки.

- `MyAndroidApp.Packaging` создает файл с расширением *.apk* для развертывания на устройстве или в эмуляторе Android. Он содержит ресурсы и файл *AndroidManifest.xml* , в которых задаются свойства манифеста. Он также содержит файл *build.xml* , который управляет процессом сборки Ant. По умолчанию он задан как начальный проект, который можно развернуть и запустить непосредственно из Visual Studio.

## <a name="build-and-run-the-default-android-native-activity-app"></a>Создание и запуск приложения Android Native Activity по умолчанию

Разработайте и запустите приложение, созданное шаблоном, чтобы проверить установку и настройку. Для первоначального теста запустите приложение в одном из профилей устройств, установленных эмулятором Android. Если вы предпочитаете тестировать приложение на другой платформе, загрузите целевой эмулятор или подключите устройство к компьютеру.

## <a name="to-build-and-run-the-default-native-activity-app"></a>Сборка и запуск приложения Native Activity по умолчанию

1. Выберите **x86** из раскрывающегося списка **платформы решения** , если он еще не выбран.

     ![Выбор x86 из раскрывающегося списка решений платформ](../cross-platform/media/cppmdd-rc-na-solution-x86.png "Выбор раскрывающегося списка решений платформ x86")

     Если список **Платформы решения** не отображается, щелкните пункт **Платформы решения** из раскрывающегося списка **Добавить или удалить кнопки** и выберите свою платформу.

1. В строке меню последовательно выберите **Сборка** > **Собрать решение**.

     В окне "Выходные данные" отобразятся выходные данные процесса сборки для двух проектов в решении.

1. Выберите один из профилей эмулятора Android в качестве цели развертывания.

     Если вы установили другие эмуляторы или подключили устройство Android, то можете выбрать их в раскрывающемся списке платформы развертывания.

1. Нажмите клавишу **F5** , чтобы начать отладку, или **клавишу** + **F5** , чтобы начать без отладки.

   Вот как выглядит приложение по умолчанию в эмуляторе Android.

   ![Эмулятор, выполняющий ваше приложение](../cross-platform/media/cppmdd-emulator-running-app.png "Эмулятор, запускающий ваше приложение")

   Visual Studio запускает эмулятор, который за несколько секунд загружает и развертывает код. После запуска приложения можно задать точки останова и использовать отладчик для проверки кода, языковых стандартов и контрольных значений.

1. Нажмите клавиши **SHIFT** + **F5** , чтобы отключить отладку.

   Эмулятор является отдельным процессом, который продолжает выполняться. Вы можете изменять, компилировать и развертывать код несколько раз в одном эмуляторе.
