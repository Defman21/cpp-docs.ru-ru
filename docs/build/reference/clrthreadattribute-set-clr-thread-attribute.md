---
title: "/CLRTHREADATTRIBUTE (Установка атрибута потока среды CLR) | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VC.Project.VCLinkerTool.CLRThreadAttribute"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "/CLRTHREADATTRIBUTE - параметр компоновщика"
  - "-CLRTHREADATTRIBUTE - параметр компоновщика"
ms.assetid: 4907e9ef-5031-446c-aecf-0a0b32fae1e8
caps.latest.revision: 14
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
caps.handback.revision: 14
---
# /CLRTHREADATTRIBUTE (Установка атрибута потока среды CLR)
[!INCLUDE[vs2017banner](../../assembler/inline/includes/vs2017banner.md)]

Явно задавать атрибут потока точки входа CLR\-программы.  
  
## Синтаксис  
  
```  
/CLRTHREADATTRIBUTE:{STA|MTA|NONE}  
```  
  
#### Параметры  
 Многопотоковое подразделение  
 Применяет атрибут MTAThreadAttribute к точке входа программы.  
  
 НЕТ  
 Эквивалентно ситуации, когда не задан параметр \/CLRTHREADATTRIBUTE.  Разрешает CLR задать стандартный атрибут потока.  
  
 Однопотоковое подразделение  
 Применяет атрибут STAThreadAttribute к точке входа программы.  
  
## Заметки  
 Установка данного атрибута потока допустима только при построении EXE\-файла, поскольку она влияет на точку ввода главного потока.  
  
 При использовании точки ввода по умолчанию \(например "main" или "wmain"\) следует указать поточную модель либо с помощью атрибута \/CLRTHREADATTRIBUTE, либо поместив атрибут потока \("STAThreadAttribute" или "MTAThreadAttribute"\) в функцию ввода по умолчанию.  
  
 При использовании точки ввода, отличной от точки ввода по умолчанию, следует указать поточную модель либо с помощью атрибута \/CLRTHREADATTRIBUTE, либо поместив атрибут потока в функцию ввода, отличную от функции ввода по умолчанию, а затем указав точку ввода, отличную от точки ввода по умолчанию, с помощью атрибута [\/ENTRY](../../build/reference/entry-entry-point-symbol.md).  
  
 Если потоковая модель, указанная в исходном коде, не согласуется с потоковой моделью, заданной с помощью атрибута \/CLRTHREADATTRIBUTE, компоновщик будет игнорировать атрибут \/CLRTHREADATTRIBUTE и будет применять ту поточную модель, которая задана в исходном коде.  
  
 Необходимо использовать однопоточную модель, например, в том случае, если CLR\-программа содержит объект СОМ, который использует однопоточную модель.  Если CLR\-программа использует многопоточную модель, она не может содержать объекты СОМ, использующие однопоточную модель.  
  
### Установка данного параметра компоновщика в среде разработки Visual Studio  
  
1.  Откройте диалоговое окно **Страницы свойств** проекта.  Дополнительные сведения см. в разделе [Открытие свойств страниц проекта](../../misc/how-to-open-project-property-pages.md).  
  
2.  Разверните узел **Свойства конфигурации**.  
  
3.  Разверните узел **Компоновщик**.  
  
4.  Выберите страницу свойств **Дополнительно**.  
  
5.  Измените значение свойства **Атрибут потока среды CLR**.  
  
### Установка данного параметра компоновщика программным способом  
  
1.  См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.CLRThreadAttribute%2A>.  
  
## См. также  
 [Настройка параметров компоновщика](../../build/reference/setting-linker-options.md)   
 [Параметры компоновщика](../../build/reference/linker-options.md)