---
description: 'Дополнительные сведения: ошибка времени выполнения C R6032'
title: Ошибка времени выполнения C R6032
ms.date: 11/04/2016
f1_keywords:
- R6032
helpviewer_keywords:
- R6032
ms.assetid: 52092a63-cc51-444a-bfc3-fad965a3558e
ms.openlocfilehash: b0fbc7730867fb6e9045adf4e5e2b8667f741784
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97275897"
---
# <a name="c-runtime-error-r6032"></a>Ошибка времени выполнения C R6032

Недостаточно места для сведений о языковых стандартах

> [!NOTE]
> Если при запуске приложения возникло это сообщение об ошибке, работа приложения была завершена из-за внутренней проблемы с памятью. Существует несколько возможных причин возникновения этой ошибки, но часто это вызвано крайне нехваткой памяти или ошибкой в программе.
>
> Для устранения этой ошибки попробуйте выполнить следующие действия:
>
> - Закройте другие запущенные приложения или перезагрузите компьютер, чтобы освободить память.
> - Используйте страницу **приложения и компоненты** или **программы и компоненты** на **панели управления** , чтобы восстановить или переустановить программу.
> - Проверьте **Центр обновления Windows** на **панели управления** для обновлений программного обеспечения.
> - Проверьте наличие обновленной версии приложения. Если проблема не исчезнет, обратитесь к поставщику приложения.

**Сведения для программистов**

Среда выполнения хранит сведения о языковом стандарте в каждом потоке, чтобы он мог обрабатывать вызовы к функциям, зависящим от языкового стандарта. Если выделение памяти для этой информации завершается ошибкой, среда выполнения не может продолжать работу, так как от нее зависят слишком много базовых средств.
