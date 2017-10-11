---
title: "Типы проектов Visual C++ | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "программы [C++], проекты"
  - "шаблоны проектов [Visual Studio], C++"
  - "комментарии TODO [C++]"
  - "проекты [C++], типы"
  - "шаблоны [C++], проекты"
  - "приложения [C++], проекты"
  - "проекты Visual C++, типы"
ms.assetid: 7337987e-1e7b-4120-9a4b-94f0401f15e7
caps.latest.revision: 20
caps.handback.revision: 20
author: "mikeblome"
ms.author: "mblome"
manager: "ghogen"
---
# Типы проектов Visual C++
[!INCLUDE[vs2017banner](../assembler/inline/includes/vs2017banner.md)]

Вы можете воспользоваться шаблоном проекта для создания базовой структуры программы, меню, панелей инструментов, значков, ссылок и инструкций `#include`, подходящих для разрабатываемого проекта. Visual Studio содержит несколько видов шаблонов проектов Visual C\+\+ и предоставляет для многих из них мастеры, позволяющие настраивать проекты во время их создания. Сразу же после создания проекта вы можете выполнить его сборку и запустить приложение. В общем случае рекомендуется периодически производить сборку по мере разработки приложения.  
  
 Использовать шаблон при создании проекта необязательно, однако в большинстве случаев это гораздо эффективнее, так как проще изменять имеющиеся файлы и структуру проекта, чем создавать их "с нуля".  
  
> [!NOTE]
>  Вы можете создать проект на языке из разряда C, используя шаблоны проектов C\+\+. Найдите в созданном проекте файлы с расширением CPP и измените его на C. Затем на странице **Свойства проекта** проекта \(а не решения\) разверните узлы **Свойства конфигурации**, **C\/C\+\+** и выберите **Дополнительно**. Измените значение параметра **Компилировать как** на **Компилировать как C код \(\/TC\)**.  
  
## Шаблоны проектов  
 Visual Studio содержит следующие шаблоны проекта Visual C\+\+.  
  
### Приложения Магазина  
  
||  
|-|  
|[Шаблоны проектов C\#, VB и C\+\+ для приложений Магазина](http://go.microsoft.com/fwlink/p/?LinkID=262279)|  
  
### ATL  
  
|Шаблон проекта|Создание проекта|  
|--------------------|----------------------|  
|Проект ATL|[Создание проекта библиотеки ATL](../atl/reference/creating-an-atl-project.md)|  
  
### CLR  
  
|Шаблон проекта|  
|--------------------|  
|[\(NOTINBUILD\)Шаблон библиотеки классов \(C\+\+\)](http://msdn.microsoft.com/ru-ru/0d779bfa-5c5a-4b10-a9d5-a6791764a78f)|  
|[Практическое руководство. Создание консольного приложения CLR.](../Topic/How%20to:%20Create%20CLR%20Console%20Applications%20\(C++-CLI\).md)|  
|[NOTINBUILD Шаблон пустого проекта CLR \(C\+\+\)](http://msdn.microsoft.com/ru-ru/f57c5572-5581-440f-b684-eec646764f08)|  
  
### Общие  
  
|Шаблон проекта|Создание проекта|  
|--------------------|----------------------|  
|Пустой проект|[Создание проектов и решений](../Topic/Creating%20Solutions%20and%20Projects.md)|  
|Специальный мастер|[Создание пользовательского мастера](../ide/creating-a-custom-wizard.md)|  
|Проект, использующий файл makefile|[Создание проекта Makefile](../ide/creating-a-makefile-project.md)|  
  
### MFC  
  
|Шаблон проекта|Создание проекта|  
|--------------------|----------------------|  
|Элемент управления ActiveX библиотеки MFC|[Создание элемента управления ActiveX MFC](../mfc/reference/creating-an-mfc-activex-control.md)|  
|Приложение MFC|[Создание приложения MFC](../mfc/reference/creating-an-mfc-application.md)|  
|Библиотека DLL MFC|[Создание проекта библиотеки DLL MFC](../mfc/reference/creating-an-mfc-dll-project.md)|  
  
### Тестирование  
  
|Шаблон проекта|Создание проекта|  
|--------------------|----------------------|  
|Управляемый тестовый проект|[Создание проекта модульного теста](../Topic/Create%20a%20unit%20test%20project.md)|  
|Проект модульного теста в машинном коде|[Модульное тестирование машинного кода с использованием обозревателя тестов](http://msdn.microsoft.com/ru-ru/8a09d6d8-3613-49d8-9ffe-11375ac4736c)|  
  
### Win32  
  
|Шаблон проекта|Создание проекта|  
|--------------------|----------------------|  
|Консольный проект Win32|[Создание консольного приложения](../windows/creating-a-console-application.md)|  
|Проект Win32|[Практическое руководство. Создание классического приложения Windows](../Topic/How%20to:%20Create%20a%20Windows%20Desktop%20Application.md)|  
  
## Комментарии TODO  
 Многие файлы, создаваемые шаблоном проекта, содержат комментарии TODO, помогающие найти места для вставки собственного исходного кода. Дополнительные сведения о добавлении кода см. в разделах [Добавление функциональных возможностей с помощью мастеров кода](../ide/adding-functionality-with-code-wizards-cpp.md) и [Working with Resource Files](../mfc/working-with-resource-files.md).  
  
## См. также  
 [Создание проектов для рабочего стола с помощью мастеров приложений](../ide/creating-desktop-projects-by-using-application-wizards.md)   
 [Использование проектов для создания приложений](http://msdn.microsoft.com/ru-ru/3339fa90-bac2-4b95-8361-662a2e0e7dfe)   
 [Проекты CLR](../ide/files-created-for-clr-projects.md)