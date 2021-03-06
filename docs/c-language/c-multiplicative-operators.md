---
description: 'Подробнее о следующем: Операторы умножения в C'
title: Операторы умножения в C
ms.date: 11/04/2016
helpviewer_keywords:
- arithmetic operators [C++], multiplicative operators
- / operator
- / operator, multiplicative operators
- remainder operator (%)
- operators [C], multiplication
- '% operator'
- slash (/) operator
- multiplication operator [C++], multiplicative operators
ms.assetid: 495471c9-319b-4eb4-bd97-039a025fd3a9
ms.openlocfilehash: 61689435c5e76238feba26d5a49ffe3530798f88
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97300272"
---
# <a name="c-multiplicative-operators"></a>Операторы умножения в C

Мультипликативные операторы выполняют операции умножения (<strong>\*</strong>), деления ( **/** ) и вычисления остатка ( **%** ).

## <a name="syntax"></a>Синтаксис

*multiplicative-expression*: &nbsp;&nbsp;&nbsp;&nbsp;*cast-expression* &nbsp;&nbsp;&nbsp;&nbsp;*multiplicative-expression* <strong>\*</strong> *cast-expression* &nbsp;&nbsp;&nbsp;&nbsp;*multiplicative-expression* **/** *cast-expression* &nbsp;&nbsp;&nbsp;&nbsp;*multiplicative-expression* **%** *cast-expression*

Операнды оператора вычисления остатка ( **%** ) должны быть целочисленными. Операторы умножения (<strong>\*</strong>) и деления ( **/** ) могут принимать операнды целочисленного типа и операнды с плавающей запятой, при этом допускаются операнды разных типов.

Мультипликативные операторы выполняют обычные арифметические преобразования над операндами. После преобразования тип результата совпадает с типом операндов.

> [!NOTE]
> Поскольку преобразования, выполняемые мультипликативными операторами, не обеспечивают условия переполнения и потери значимости, данные могут быть потеряны, если результат мультипликативной операции невозможно представить в типе операндов после преобразования.

Ниже описаны мультипликативные операторы C.

|Оператор|Описание|
|--------------|-----------------|
|<strong>\*</strong>|Оператор умножения выполняет умножение двух операндов.|
|**/**|Оператор деления выполняет деление первого операнда на второй. Если два целочисленных операнда делятся друг на друга и результат не является целым числом, он округляется в соответствии со следующими правилами.<br/><br/>— Согласно стандарту ANSI C результат деления на 0 не определен. Во время компиляции или выполнения компилятор Microsoft C выдает ошибку.<br/><br/>— Если оба операнда положительные или не имеют знака, дробная часть результата отбрасывается.<br/><br/>— Если один из операндов отрицательный, результатом операции может быть наибольшее целое число, меньшее или равное частному от деления, или наименьшее целое число, большее или равное частному от деления. Это определяется реализацией. (См. раздел "Для систем Майкрософт" ниже.)|
|**%**|Результат выполнения оператора вычисления остатка — остаток от деления первого операнда на второй. При неточном делении результат определяется следующими правилами.<br/><br/>— Если правый операнд равен нулю, результат будет неопределенным.<br/><br/>— Если оба операнда положительные или не имеют знака, результат будет положительным.<br/><br/>— Если один из операндов отрицательный и результат неточный, результат определяется реализацией. (См. раздел "Для систем Майкрософт" ниже.)|

### <a name="microsoft-specific"></a>Специально для систем Майкрософт

Если при делении один из операндов отрицательный, дробная часть результата отбрасывается.

Если при делении с использованием оператора вычисления остатка один из операндов отрицательный, знак результата совпадает со знаком делимого (первого операнда выражения).

## <a name="examples"></a>Примеры

Для приведенных ниже примеров используются следующие объявления:

```
int i = 10, j = 3, n;
double x = 2.0, y;
```

В следующей инструкции используется оператор умножения.

```
y = x * i;
```

В этом примере `x` умножается на `i` и получается значение 20.0. Результат имеет тип **`double`** .

```
n = i / j;
```

В этом примере 10 делится на 3. Дробная часть результата отбрасывается и получается целое значение 3.

```
n = i % j;
```

В этой инструкции переменной `n` присваивается значение целочисленного остатка (1) от деления 10 на 3.

**Блок, относящийся только к системам Microsoft**

Знак остатка совпадает со знаком делимого. Пример:

```
50 % -6 = 2
-50 % 6 = -2
```

В каждом случае значения `50` и `2` имеют один и тот же знак.

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также

[Операторы умножения и оператор модуля](../cpp/multiplicative-operators-and-the-modulus-operator.md)
