---
title: "R6009 ошибку во время выполнения C | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: error-reference
f1_keywords:
- R6009
dev_langs:
- C++
helpviewer_keywords:
- R6009
ms.assetid: edfb1f8b-3807-48f4-a994-318923b747ae
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: ghogen
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3168772cbb7e8127523bc2fc2da5cc9b4f59beb8
ms.openlocfilehash: f0a5401b32b5bd2918b316a8dd1b16ec3db1e8f3
ms.contentlocale: ru-ru
ms.lasthandoff: 02/24/2017

---
# <a name="c-runtime-error-r6009"></a>R6009 ошибка времени выполнения C
Недостаточно места для среды  
  
> [!NOTE]
>  Если появится следующее сообщение об ошибке при выполнении приложения приложения была завершена из-за проблемы внутреннюю память. Существует несколько возможных причин возникновения данной ошибки, но часто причиной является причиной слишком мало памяти слишком большого объема памяти, занимаемого переменные среды или ошибки в программе.  
>   
>  Для устранения этой ошибки попробуйте выполнить следующие действия:  
>   
>  -   Закройте другие запущенные приложения или перезагрузите компьютер, чтобы освободить память.  
> -   Используйте **приложения и компоненты** или **программы и компоненты** страницы в **панели управления** восстановите или переустановите программу.  
> -   Проверьте **обновление Windows** в **панели управления** для обновлений программного обеспечения.  
> -   Проверьте наличие обновленной версии приложения. Если проблема сохранится, обратитесь к поставщику приложения.  
  
 **Сведения для программистов**  
  
 Было недостаточно памяти для загрузки программы, но недостаточно памяти для создания **envp** массива.  Причиной может быть очень нехватки памяти или использования переменной среды слишком большое. Рассмотрите одну из следующих решений.  
  
-   Увеличьте объем доступной памяти для программы.  
  
-   Уменьшите число и размер аргументов командной строки.  
  
-   Уменьшите размер среды, удалив неиспользуемые переменные.