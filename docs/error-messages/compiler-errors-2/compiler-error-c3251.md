---
title: "Ошибка компилятора C3251 | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-tools
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- C3251
dev_langs:
- C++
helpviewer_keywords:
- C3251
ms.assetid: 541c163e-5ee9-457c-a1e5-da860788b10d
caps.latest.revision: 6
author: corob-msft
ms.author: corob
manager: ghogen
ms.translationtype: MT
ms.sourcegitcommit: 35b46e23aeb5f4dbfd2a0dd44b906389dd5bfc88
ms.openlocfilehash: f17f45a35f9ddd1b3270b484a49c603bee92f8f7
ms.contentlocale: ru-ru
ms.lasthandoff: 10/10/2017

---
# <a name="compiler-error-c3251"></a>Ошибка компилятора C3251
нельзя вызвать метод базового класса для экземпляра типа значения  
  
 Следующая ошибка происходит потому, что `GetClass` является членом `Microsoft.Runtime.Object`, а не `Microsoft.Runtime.Integer4`.