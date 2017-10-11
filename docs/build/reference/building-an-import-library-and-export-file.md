---
title: "Построение библиотеки импорта и файла экспорта | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VC.Project.VCLibrarianTool.ModuleDefinitionFile"
  - "VC.Project.VCLibrarianTool.ExportNamedFunctions"
  - "VC.Project.VCLibrarianTool.GenerateDebug"
  - "VC.Project.VCLibrarianTool.ForceSymbolReferences"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "LIB-файлы"
  - "/DEF - параметр управления библиотекой"
  - "/EXPORT - параметр управления библиотекой"
  - "/INCLUDE - параметр управления библиотекой"
  - "/OUT - параметр управления библиотекой"
  - "DEF - параметр управления библиотекой"
  - "-DEF - параметр управления библиотекой"
  - "EXP-файлы"
  - "EXPORT - параметр управления библиотекой"
  - "-EXPORT - параметр управления библиотекой"
  - "данные - экспортирование"
  - "данные - экспортирование, EXP-файлы - экспорт"
  - "библиотеки - импорт, построение"
  - "INCLUDE - параметр управления библиотекой"
  - "-INCLUDE - параметр управления библиотекой"
  - "OUT - параметр управления библиотекой"
  - "-OUT - параметр управления библиотекой"
ms.assetid: 2fe4f30a-1dd6-4b05-84b5-0752e1dee354
caps.latest.revision: 8
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
caps.handback.revision: 8
---
# Построение библиотеки импорта и файла экспорта
[!INCLUDE[vs2017banner](../../assembler/inline/includes/vs2017banner.md)]

Для построения библиотеки импорта и файла экспорта используется следующий синтаксис:  
  
```  
LIB /DEF[:deffile] [options] [objfiles] [libraries]  
```  
  
 В случае, когда указан параметр \/DEF, программа LIB создает выходные файлы по спецификациям экспорта, указанным в команде LIB.  Существует три метода указания экспортов; далее они перечислены в рекомендуемом порядке использования:  
  
1.  Определение **\_\_declspec\(dllexport\)** в одном из *объектных файлов* или *библиотек*;  
  
2.  Указание параметра \/EXPORT:*имя* в командной строке LIB;  
  
3.  Определение в операторе **EXPORTS** в DEF\-файле `deffile`  
  
 Это те же методы, которые применяются для указания экспортов при компоновке экспортирующей программы.  В программе может использоваться сразу несколько методов.  Можно указывать части команды LIB \(например, несколько *объектных файлов* или спецификаций \/EXPORT\) в командном файле команды LIB, таким же образом, как и в команде LINK.  
  
 Для построения библиотеки импорта и файла экспорта применяются следующие параметры:  
  
 \/OUT: *импорт*  
 Заменяет имя выходного файла, используемое по умолчанию, для создаваемой библиотеки *импорт*.  Если параметр \/OUT не задан, по умолчанию в качестве базового имени используется имя первого объектного файла или библиотеки в команде LIB; в качестве расширения используется LIB.  Файлу экспорта присваивается то же базовое имя, что и библиотеке импорта; в качестве расширения используется EXP.  
  
 \/EXPORT: *имязаписи*\[\= *внутреннееимя*\]\[,@ `ordinal`\[, **NONAME**\]\]\[, **DATA**\]  
 Экспортирует функцию из программы для того, чтобы другие программы могли вызывать эту функцию.  Можно также экспортировать данные \(используя ключевое слово **DATA**\).  Экспорты обычно определяются в библиотеке DLL.  
  
 *Имязаписи* — это имя функции или компонента данных в том виде, в котором оно будет использоваться вызывающей программой.  Кроме того, можно указать *внутреннееимя* для функции, известной определяющей программе; по умолчанию *внутреннееимя* тождественно *именизаписи*.  Параметр `ordinal` задает индекс в таблице экспорта в пределах от 1 до 65 535; если не задать параметр `ordinal`, то его значение будет задано программой LIB.  Ключевое слово **NONAME** экспортирует функцию только по порядковому номеру, без имени *имязаписи*.  Ключевое слово **DATA** используется только для экспорта объектов данных.  
  
 \/INCLUDE: `symbol`  
 Добавляет указанный символ в таблицу символов.  Этот параметр позволяет принудительно включить объект, который не будет включен в библиотеку без использования этого параметра.  
  
 Обратите внимание, что при предварительном создании библиотеки импорта перед созданием DLL\-файла для построения библиотеки импорта необходимо использовать тот же набор объектных файлов, что и при построении DLL\-файла.  
  
## См. также  
 [Работа с библиотеками импорта и файлами экспорта](../../build/reference/working-with-import-libraries-and-export-files.md)