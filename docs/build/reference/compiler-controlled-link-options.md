---
title: "Управляемые компилятором параметры LINK | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "link"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "cl.exe - компилятор [C++], управление компоновщиком"
  - "cl.exe - компилятор [C++], возможности управления компоновщиком"
  - "LINK - средство [C++], управляемые компилятором параметры"
  - "компоновщик [C++], CL - элемент управления компоновщиком"
  - "связывание [C++], под воздействием возможностей CL"
ms.assetid: e4c03896-c99c-4599-8502-e0f4bebe69d0
caps.latest.revision: 8
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
caps.handback.revision: 8
---
# Управляемые компилятором параметры LINK
[!INCLUDE[vs2017banner](../../assembler/inline/includes/vs2017banner.md)]

CL\-компилятор автоматически вызывает LINK, если не задан параметр \/c.  CL предоставляет определенные возможности управления компоновщиком с помощью параметров и аргументов командной строки.  В следующей таблице перечислены функции CL\-компилятора, которые позволяют влиять на компоновку.  
  
|Спецификация CL\-компилятора|Воздействие CL\-компилятора на LINK|  
|----------------------------------|-----------------------------------------|  
|Любое расширение имени файла кроме C, CXX, CPP или DEF|Позволяет передать компоновщику LINK имя файла в качестве входных данных|  
|*имя\_файла*.def|Передает \/DEF:*имя\_файла*.def|  
|\/F`number`|Передает \/STACK:`number`|  
|\/Fd*имя\_файла*|Передает \/PDB:*имя\_файла*|  
|\/Fe*имя\_файла*|Передает \/OUT:*имя\_файла*|  
|\/Fm*имя\_файла*|Передает \/MAP:*имя\_файла*|  
|\/Gy|Создает пакет функций \(COMDAT\); обеспечивает компоновку на уровне функций|  
|\/LD|Передает \/DLL|  
|\/LDd|Передает \/DLL|  
|\/link|Передает компоновщику LINK остаток командной строки|  
|\/MD или \/MT|Размещает в OBJ\-файле имя библиотеки по умолчанию|  
|\/MDd или \/MTd|Размещает в OBJ\-файле имя библиотеки по умолчанию.  Определяет символ **\_DEBUG**|  
|\/nologo|Передает \/NOLOGO|  
|\/Zd|Передает \/DEBUG|  
|\/Zi или \/Z7|Передает \/DEBUG|  
|\/Zl|Пропускает в OBJ\-файле имя библиотеки по умолчанию.|  
  
 Дополнительные сведения см. в разделе [Параметры компилятора](../../build/reference/compiler-options.md).  
  
## См. также  
 [Настройка параметров компоновщика](../../build/reference/setting-linker-options.md)   
 [Параметры компоновщика](../../build/reference/linker-options.md)