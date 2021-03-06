---
description: 'Дополнительные сведения: ошибки компилятора, C3200 через C3299'
title: Ошибки компилятора с C3200 по C3299
ms.date: 04/21/2019
f1_keywords:
- C3220
- C3221
- C3245
- C3249
- C3250
- C3256
- C3257
- C3258
- C3259
- C3260
- C3261
- C3263
- C3267
- C3281
- C3294
helpviewer_keywords:
- C3220
- C3221
- C3245
- C3249
- C3250
- C3256
- C3257
- C3258
- C3259
- C3260
- C3261
- C3263
- C3267
- C3281
- C3294
ms.assetid: 6b3104f6-63bc-4823-b6f3-b8a16be4b87f
ms.openlocfilehash: e54d980634372099d76d9f30020f68f3f4affb59
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97238665"
---
# <a name="compiler-errors-c3200-through-c3299"></a>Ошибки компилятора с C3200 по C3299

В статьях этого раздела документации описывается подмножество сообщений об ошибках, создаваемых компилятором.

[!INCLUDE[error-boilerplate](../../error-messages/includes/error-boilerplate.md)]

## <a name="error-messages"></a>Сообщения об ошибках

|Error|Сообщение|
|-----------|-------------|
|[Ошибка компилятора C3200](compiler-error-c3200.md)|"*тип*": недопустимый аргумент шаблона для параметра шаблона "*параметр*", требуется шаблон класса|
|[Ошибка компилятора C3201](compiler-error-c3201.md)|список параметров шаблона для шаблона класса "*шаблон*" не соответствует списку параметров шаблона для параметра шаблона "*параметр*"|
|[Ошибка компилятора C3202](compiler-error-c3202.md)|"*идентификатор*": недопустимый аргумент по умолчанию; требуется шаблон класса|
|[Ошибка компилятора C3203](compiler-error-c3203.md)|"*идентификатор*": шаблон или универсальный класс не может использоваться в качестве шаблона или универсального аргумента для шаблона или универсального параметра "*параметр*", ожидается реальный тип|
|[Ошибка компилятора C3204](compiler-error-c3204.md)|"*функция*" не может быть вызвана из блока catch|
|[Ошибка компилятора C3205](compiler-error-c3205.md)|отсутствует список аргументов для параметра шаблона шаблона "*идентификатор*"|
|[Ошибка компилятора C3206](compiler-error-c3206.md)|"*функция*": недопустимый шаблон или универсальный аргумент для "*template*", отсутствует список аргументов шаблона или универсального аргумента в шаблоне класса/универсальный "*тип*"|
|[Ошибка компилятора C3207](compiler-error-c3207.md)|"*функция*": недопустимый аргумент шаблона для "*Parameter*", требуется шаблон класса|
|[Ошибка компилятора C3208](compiler-error-c3208.md)|"*функция*": список параметров шаблона для шаблона класса "*шаблон*" не соответствует списку параметров шаблона для параметра шаблона "*параметр*"|
|[Ошибка компилятора C3209](compiler-error-c3209.md)|"*тип*": универсальный класс должен быть управляемым классом/WinRT|
|[Ошибка компилятора C3210](compiler-error-c3210.md)|"*идентификатор*": объявление доступа может применяться только к члену базового класса|
|[Ошибка компилятора C3211](compiler-error-c3211.md)|"*функция*": явная специализация использует синтаксис частичной специализации, вместо этого используйте шаблон <> |
|[Ошибка компилятора C3212](compiler-error-c3212.md)|"*функция*": явная специализация члена шаблона должна быть членом явной специализации|
|[Ошибка компилятора C3213](compiler-error-c3213.md)|доступность базового класса "*класс*" ниже доступности "*derived_class*"|
|[Ошибка компилятора C3214](compiler-error-c3214.md)|"*аргумент*": недопустимый аргумент типа для универсального параметра "*параметр*" универсального *типа "тип*", не соответствует ограничению "*ограничение*"|
|[Ошибка компилятора C3215](compiler-error-c3215.md)|"*Constraint1*": параметр универсального типа уже ограничен "*constraint2*"|
|[Ошибка компилятора C3216](compiler-error-c3216.md)|ограничение должно быть универсальным параметром, а не "*Type*"|
|[Ошибка компилятора C3217](compiler-error-c3217.md)|"*параметр*": универсальный параметр не может быть ограничен в этом объявлении|
|[Ошибка компилятора C3218](compiler-error-c3218.md)|"*тип*": тип не допускается в качестве ограничения|
|[Ошибка компилятора C3219](compiler-error-c3219.md)|"*параметр*": универсальный параметр не может быть ограничен несколькими не-интерфейсами: "*тип*"|
|Ошибка компилятора C3220|"*интерфейс*": интерфейс не может иметь ProgID|
|Ошибка компилятора C3221|"*член*": для члена не допускается использование нескольких атрибутов "default" и "Case"|
|[Ошибка компилятора C3222](compiler-error-c3222.md)|"*функция*": невозможно объявить аргументы по умолчанию для функций-членов типа Managed/WinRT или универсальных функций|
|[Ошибка компилятора C3223](compiler-error-c3223.md)|"*свойство*": нельзя применить typeid к свойству|
|[Ошибка компилятора C3224](compiler-error-c3224.md)|"*тип*": нет перегруженного универсального класса, принимающего аргументы универсального типа "*число*"|
|[Ошибка компилятора C3225](compiler-error-c3225.md)|аргумент универсального типа для "*аргумента*" не может быть "*тип*", он должен быть типом значения или маркером ссылочного типа|
|[Ошибка компилятора C3226](compiler-error-c3226.md)|Объявление шаблона недопустимо внутри универсального объявления|
|[Ошибка компилятора C3227](compiler-error-c3227.md)|"*тип*": нельзя использовать "*operator*" для выделения универсального типа|
|[Ошибка компилятора C3228](compiler-error-c3228.md)|"*функция*": аргумент универсального типа для "*аргумента*" не может быть "*тип*", он должен быть типом значения или типом обработчика|
|[Ошибка компилятора C3229](compiler-error-c3229.md)|"*тип*": косвенные обращения к параметру универсального типа не допускаются|
|[Ошибка компилятора C3230](compiler-error-c3230.md)|"*функция*": аргумент типа шаблона для "*Argument*" не может содержать параметр универсального типа: "*тип*"|
|[Ошибка компилятора C3231](compiler-error-c3231.md)|"*тип*": аргумент типа шаблона не может использовать параметр универсального типа|
|[Ошибка компилятора C3232](compiler-error-c3232.md)|"*параметр*": параметр универсального типа нельзя использовать в полном имени|
|[Ошибка компилятора C3233](compiler-error-c3233.md)|"*тип*": параметр универсального типа уже ограничен|
|[Ошибка компилятора C3234](compiler-error-c3234.md)|универсальный класс нельзя вывести из параметра универсального типа|
|[Ошибка компилятора C3235](compiler-error-c3235.md)|"*специализация*": явная или частичная специализация универсального класса не допускается|
|[Ошибка компилятора C3236](compiler-error-c3236.md)|явное создание экземпляра универсального класса не допускается|
|[Ошибка компилятора C3237](compiler-error-c3237.md)|"*класс*": универсальный класс не может быть пользовательским атрибутом|
|[Ошибка компилятора C3238](compiler-error-c3238.md)|"*тип*": тип с таким именем уже перенаправлен в сборку "*Assembly*"|
|[Ошибка компилятора C3239](compiler-error-c3239.md)|"*тип*": указатель на внутренний или закрепление указатель запрещен средой CLR|
|[Ошибка компилятора C3240](compiler-error-c3240.md)|"*идентификатор*": должна быть неперегруженной абстрактной функцией-членом типа "*тип*"|
|[Ошибка компилятора C3241](compiler-error-c3241.md)|"*член*": Этот метод не был введен с помощью "*Interface*"|
|[Ошибка компилятора C3242](compiler-error-c3242.md)|"*функция*": можно явно переопределить только виртуальные функции|
|[Ошибка компилятора C3243](compiler-error-c3243.md)|ни одна из функций перегрузки не появилась в "*Interface*"|
|[Ошибка компилятора C3244](compiler-error-c3244.md)|"*член*": Этот метод был введен "*интерфейс1*", а не "*интерфейс2*"|
|Ошибка компилятора C3245|"*функция*": для использования шаблона переменной требуется список аргументов шаблона|
|[Ошибка компилятора C3246](compiler-error-c3246.md)|"*класс*": не может наследовать от "*base_class*", так как он был объявлен как "*наследование*"|
|[Ошибка компилятора C3247](compiler-error-c3247.md)|"*coclass*": coclass не может наследовать от другого класса "*base_class*"|
|[Ошибка компилятора C3248](compiler-error-c3248.md)|Является устаревшей. "*функция*": функция, объявленная как "Sealed", не может быть переопределена *функцией "Function*"|
|Ошибка компилятора C3249|Недопустимый оператор или часть выражения для функции "constexpr"|
|Ошибка компилятора C3250|"*объявление*": объявление не допускается в теле функции "constexpr"|
|[Ошибка компилятора C3251](compiler-error-c3251.md)|нельзя вызвать метод базового класса для экземпляра типа значения|
|[Ошибка компилятора C3252](compiler-error-c3252.md)|"*функция*": невозможно уменьшить доступность виртуального метода в управляемом типе/WinRT|
|[Ошибка компилятора C3253](compiler-error-c3253.md)|"*функция*": ошибка с явным переопределением|
|[Ошибка компилятора C3254](compiler-error-c3254.md)|"*функция*": класс содержит явное переопределение "*функция*", но не является производным от интерфейса, содержащего объявление функции|
|[Ошибка компилятора C3255](compiler-error-c3255.md)|"*тип*": невозможно динамически выделить этот объект типа значения в собственной куче|
|Ошибка компилятора C3256|"*функция*": использование переменной не приводит к созданию константного выражения|
|Ошибка компилятора C3257|Является устаревшей.|
|Ошибка компилятора C3258|Является устаревшей.|
|Ошибка компилятора C3259|функции "constexpr" могут иметь только один оператор return|
|Ошибка компилятора C3260|"*токен*": пропуск непредвиденных токенов перед телом лямбда-выражения|
|Ошибка компилятора C3261|функция, возвращающая управляемый массив/WinRT, должна содержать скобки массива в конце объявления: "*идентификатор*(...)" []'|
|[Ошибка компилятора C3262](compiler-error-c3262.md)|Недопустимое индексирование массива: *числовые* размеры, указанные для *числового* массива "*тип*"|
|Ошибка компилятора C3263|Является устаревшей.|
|[Ошибка компилятора C3264](compiler-error-c3264.md)|"*идентификатор*": конструктор класса не может иметь тип возвращаемого значения|
|[Ошибка компилятора C3265](compiler-error-c3265.md)|Невозможно объявить управляемый "*managed_construct*" в неуправляемом "*unmanaged_construct*"|
|[Ошибка компилятора C3266](compiler-error-c3266.md)|"*функция*": конструктор класса должен иметь список параметров "void"|
|Ошибка компилятора C3267|Является устаревшей.|
|[Ошибка компилятора C3268](compiler-error-c3268.md)|"*функция*": универсальная функция или функция-член универсального класса не может иметь переменный список параметров|
|[Ошибка компилятора C3269](compiler-error-c3269.md)|"*функция*": функция-член управляемого типа/WinRT не может быть объявлена с "..."|
|[Ошибка компилятора C3270](compiler-error-c3270.md)|"*поле*": атрибут FieldOffset может использоваться только в контексте StructLayout (LayoutKind:: explicit)|
|[Ошибка компилятора C3271](compiler-error-c3271.md)|"*поле*": недопустимое значение "*Number*" для атрибута FieldOffset|
|[Ошибка компилятора C3272](compiler-error-c3272.md)|"*символ*": символу требуется атрибут FieldOffset, так как он является членом структуры или класса *TYPE_NAME* определенный с помощью StructLayout (LayoutKind:: explicit)|
|[Ошибка компилятора C3273](compiler-error-c3273.md)|"*ключевое слово*": недопустимый блок try C++|
|[Ошибка компилятора C3274](compiler-error-c3274.md)|Finally/&#95;&#95;, наконец, без соответствующего try|
|[Ошибка компилятора C3275](compiler-error-c3275.md)|"*идентификатор*": нельзя использовать этот символ без квалификатора|
|[Ошибка компилятора C3276](compiler-error-c3276.md)|"*ключевое слово*": выход из блока finally/&#95;&#95;finally имеет неопределенное поведение во время обработки завершения|
|[Ошибка компилятора C3277](compiler-error-c3277.md)|невозможно определить неуправляемое *перечисление*"enum" внутри управляемого "*тип*"|
|[Ошибка компилятора C3278](compiler-error-c3278.md)|прямой вызов интерфейса или чистого метода "*функция*" завершится ошибкой во время выполнения|
|[Ошибка компилятора C3279](compiler-error-c3279.md)|Частичные и явные специализации, а также явные создания экземпляров шаблонов классов, объявленные в пространстве имен CLI, запрещены|
|[Ошибка компилятора C3280](compiler-error-c3280.md)|"*функция*": функция-член управляемого типа не может быть скомпилирована как неуправляемая функция|
|Ошибка компилятора C3281|"*функция*": глобальный оператор не может иметь тип управляемого или WinRT "*тип*" в сигнатуре|
|[Ошибка компилятора C3282](compiler-error-c3282.md)|Списки универсальных параметров могут использоваться только в управляемых классах, структурах или функциях WinRT|
|[Ошибка компилятора C3283](compiler-error-c3283.md)|"*Interface*": интерфейс не может иметь конструктор экземпляров|
|[Ошибка компилятора C3284](compiler-error-c3284.md)|ограничения для универсального параметра "*параметр*" функции "*декларатор*" должны соответствовать ограничениям для универсального параметра "*параметр*" функции "*декларатор*"|
|[Ошибка компилятора C3285](compiler-error-c3285.md)|Оператор for each не может использоваться с переменными типа "*тип*"|
|[Ошибка компилятора C3286](compiler-error-c3286.md)|"*спецификатор*": переменная итерации не может содержать спецификаторы класса хранения|
|[Ошибка компилятора C3287](compiler-error-c3287.md)|тип "*тип*" (тип возвращаемого значения GetEnumerator) должен иметь подходящую общую функцию-член MoveNext и открытое свойство Current|
|[Ошибка компилятора C3288](compiler-error-c3288.md)|"*тип*": недопустимая разыменование типа обработчика|
|[Ошибка компилятора C3289](compiler-error-c3289.md)|"*идентификатор*": тривиальное свойство не может быть проиндексировано|
|[Ошибка компилятора C3290](compiler-error-c3290.md)|"*тип*": тривиальное свойство не может иметь ссылочный тип|
|[Ошибка компилятора C3291](compiler-error-c3291.md)|"default": не может быть именем тривиального свойства|
|[Ошибка компилятора C3292](compiler-error-c3292.md)|пространство имен CLI нельзя открыть повторно|
|[Ошибка компилятора C3293](compiler-error-c3293.md)|"*идентификатор*": используйте "default" для доступа к свойству по умолчанию (индексатору) для класса "*класс*"|
|Ошибка компилятора C3294|Является устаревшей.|
|[Ошибка компилятора C3295](compiler-error-c3295.md)|*спецификатор*"#pragma" может использоваться только в глобальной области видимости или область пространства имен|
|[Ошибка компилятора C3296](compiler-error-c3296.md)|"*идентификатор*": свойство с таким именем уже существует|
|[Ошибка компилятора C3297](compiler-error-c3297.md)|" *constraint2*": невозможно использовать " *Constraint1*" как ограничение, так как " *Constraint1*" имеет ограничение значения|
|[Ошибка компилятора C3298](compiler-error-c3298.md)|" *Constraint1*": нельзя использовать " *constraint2*" в качестве ограничения, так как " *constraint2*" имеет ограничение ref, а " *Constraint1*" имеет ограничение значения|
|[Ошибка компилятора C3299](compiler-error-c3299.md)|" *функция*": невозможно указать ограничения, они унаследованы от базового метода|

## <a name="see-also"></a>См. также раздел

[Ошибки и предупреждения для компилятора C/C++ и средств сборки](../compiler-errors-1/c-cpp-build-errors.md) \
[Ошибки компилятора с C2000 по C3999](../compiler-errors-1/compiler-errors-c2000-c3999.md)
