---
description: 'Дополнительные сведения: Ошибка средств компоновщика LNK2013'
title: Ошибка средств компоновщика LNK2013
ms.date: 11/04/2016
f1_keywords:
- LNK2013
helpviewer_keywords:
- LNK2013
ms.assetid: 21408e2d-3f56-4d1f-a031-00df70785ed4
ms.openlocfilehash: 51b754e19656ad8ec7ef1686605086b6e4a41853
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97338462"
---
# <a name="linker-tools-error-lnk2013"></a>Ошибка средств компоновщика LNK2013

Переполнение адресной привязки для типа адресной привязки. Целевой объект "имя символа" выходит за пределы допустимого диапазона

Компоновщик не может поместить необходимый адрес или смещение в указанную инструкцию, так как целевой символ находится далеко от расположения инструкции.

Эту проблему можно устранить, создав несколько образов или используя параметр [/Order](../../build/reference/order-put-functions-in-order.md) , чтобы инструкция и цель были ближе друг к другу.

Если имя символа является пользовательским символом (а не сгенерированным компилятором символом), для устранения ошибки можно также выполнить следующие действия:

- Измените статическую функцию, чтобы она не была статической.

- Переименуйте раздел кода, содержащий статическую функцию, так, чтобы она совпадала с вызывающей стороной.

Используйте `DUMPBIN /SYMBOLS` , чтобы определить, является ли функция статической.
