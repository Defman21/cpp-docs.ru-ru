---
title: "Справочник по языку C++ | Документы Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- cpp-language
ms.tgt_pltfrm: 
ms.topic: 'index-page '
dev_langs:
- C++
helpviewer_keywords:
- language reference
- C++, language reference
- language reference, Visual C++
- Visual C++, language reference
ms.assetid: 4be9cacb-c862-4391-894a-3a118c9c93ce
caps.latest.revision: 14
author: mikeblome
ms.author: mblome
manager: ghogen
ms.translationtype: HT
ms.sourcegitcommit: 6ffef5f51e57cf36d5984bfc43d023abc8bc5c62
ms.openlocfilehash: 241ae5abb680d6d8142fca93661c413bde57ace1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/25/2017

---
# <a name="c-language-reference"></a>Справочник по языку C++
В этом справочнике описывается язык программирования С++ в том виде, в котором он реализован в Microsoft Visual C++. На основе *аннотированного справочного руководства по C++* Эллис (Margaret Ellis) и Страуструп (Bjarne Stroustrup) и ANSI/ISO C++ международного стандарта (ISO/IEC FDIS 14882). Включены реализации компонентов языка С++ корпорацией Майкрософт.  

Обзор Modern C++ приемы программирования см. в разделе [Добро пожаловать в C++](welcome-back-to-cpp-modern-cpp.md).
  
 Для быстрого поиска ключевого слова или оператора обращайтесь к следующим таблицам:  
  
-   [Ключевые слова C++](../cpp/keywords-cpp.md)  
  
-   [Операторы C++](../cpp/cpp-built-in-operators-precedence-and-associativity.md)  
  
## <a name="in-this-section"></a>Содержание  

 [Лексические соглашения](../cpp/lexical-conventions.md)  
 Основные лексические элементы программ на C++: токены, комментарии, операторы, ключевые слова, знаки пунктуации, литералы. Кроме того, трансляция файлов, приоритет и ассоциативность операторов.  
  
 [Основные понятия](../cpp/basic-concepts-cpp.md)  
 Область, компоновка, запуск и завершение программы, классы хранения и типы.  
  
 [Стандартные преобразования](../cpp/standard-conversions.md)  
 Преобразования между встроенными, или "фундаментальными", типами. Кроме того, арифметические преобразования и преобразования между типами указателей, ссылочными типами и типами указателей на члены.  
  
 [Операторы, приоритет и ассоциативность операторов](../cpp/cpp-built-in-operators-precedence-and-associativity.md)  
 Операторы в C++.  
  
 [Выражения](../cpp/expressions-cpp.md)  
 Типы выражений, семантика выражений, справочные разделы по операторам, приведению типов и операторам приведения, сведения о типах времени выполнения.  
  
 [Лямбда-выражения](../cpp/lambda-expressions-in-cpp.md)  
 Метод программирования, с помощью которого неявно определяется класс объекта функции и создается объект функции этого типа класса.  
  
 [Операторы](../cpp/statements-cpp.md)  
 Операторы выражений, пустые операторы, составные операторы, операторы выбора, операторы итераций, операторы перехода и операторы объявления.  
  
 [Объявления и определения](declarations-and-definitions-cpp.md)  
 Спецификаторы классов хранения, определения функций, инициализации, перечисления, объявления классов, структур и объединений и объявления typedef. Кроме того, встраиваемые функции, ключевое слово const, пространства имен.  
  
 [Деклараторы](http://msdn.microsoft.com/en-us/8a7b9b51-92bd-4ac0-b3fe-0c4abe771838)  
 Часть оператора объявления, где указывается имя объекта, типа или функции. Абстрактные деклараторы, имена типов, инициализаторы, объявления и определения функций, массивы, ссылки.  
  
 [Классы, структуры и объединения](../cpp/classes-and-structs-cpp.md)  
 Вводные сведения о классах, структурах и объединениях. Кроме того функции-члены, специальные функции-члены, данные-члены, битовые поля, этот указатель, вложенные классы.  
  
 [Производные классы](../cpp/inheritance-cpp.md)  
 Одиночное и множественное наследование, виртуальные функции, многочисленные базовые классы, абстрактные классы, правила областей. Кроме того, к __super и \__interface ключевые слова.  
  
 [Управление доступом к членам](../cpp/member-access-control-cpp.md)  
 Управление доступом к членам класса: ключевые слова public, private и protected. Дружественные функции и классы.  
  
 [Перегрузка](operator-overloading.md)  
 Перегруженные операторы, правила перегрузки операторов.  
  
 [Обработка исключений](../cpp/exception-handling-in-visual-cpp.md)  
 Обработка исключений в C++, структурированная обработка исключений (SEH), ключевые слова, используемые при написании операторов обработки исключений.  
  
 [Утверждение и предоставляемые пользователем сообщения](../cpp/assertion-and-user-supplied-messages-cpp.md)  
 Директива `#error`, ключевое слово `static_assert`, макрос `assert`.  
  
 [Шаблоны](../cpp/templates-cpp.md)  
 Спецификации шаблонов, шаблоны функций, шаблоны классов, ключевое слово typename, шаблоны и макросы, шаблоны и интеллектуальные указатели.  
  
 [Обработка событий](../cpp/event-handling.md)  
 Объявление событий и обработчиков событий.  
  
 [Модификаторы, используемые в системах Майкрософт](../cpp/microsoft-specific-modifiers.md)  
 Модификаторы, используемые в Microsoft C++. Память адресации, соглашения о вызовах, функции с атрибутом naked, расширенные атрибуты классов хранения (__declspec), \__w64.  
  
 [Встроенный сборщик](../assembler/inline/inline-assembler.md)  
 Использование языка ассемблера и C++ в блоках __asm.  
  
 [Поддержка COM компилятора](../cpp/compiler-com-support.md)  
 Справочник по характерным для систем Microsoft классам и глобальным функциям, используемым для поддержки типов модели COM.  
  
 [Расширения Майкрософт](../cpp/microsoft-extensions.md)  
 Расширения Майкрософт для C++.  
  
 [Нестандартное поведение](../cpp/nonstandard-behavior.md)  
 Сведения о нестандартном поведении компилятора Visual C++.  

 [Добро пожаловать назад в C++](welcome-back-to-cpp-modern-cpp.md) Общие сведения о современных особенностях программирования на C++ и рекомендации по написанию программ безопасном правильный и эффективный.
  
## <a name="related-sections"></a>Связанные разделы  
 [Расширения компонентов для платформ среды выполнения](../windows/component-extensions-for-runtime-platforms.md)  
 Справочный материал по использованию Visual C++ в среде CLR.  
  
 [Справочные сведения о сборке C/C++](../build/reference/c-cpp-building-reference.md)  
 Параметры компилятора, параметры компоновщика и другие средства сборки.  
  
 [Справочник по препроцессору в C/C++](../preprocessor/c-cpp-preprocessor-reference.md)  
 Справочный материал по прагма-директивам, директивам препроцессора, предопределенным макросам и препроцессору.  
  
 [Справочные материалы по библиотекам Visual C++](../standard-library/cpp-standard-library-reference.md)  
 Список ссылок на начальные страницы справочников по различным библиотекам Visual C++.  
  
## <a name="see-also"></a>См. также  
 [Справочник по языку C#](../c-language/c-language-reference.md)