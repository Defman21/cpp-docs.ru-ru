---
description: Дополнительные сведения о:/Arch (x64)
title: /arch (x64)
ms.date: 10/01/2019
ms.assetid: ecda22bf-5bed-43f4-99fb-88aedd83d9d8
ms.openlocfilehash: 1e9670cdea49c06eda6575fe2cea872072a4e332
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97183078"
---
# <a name="arch-x64"></a>/arch (x64)

Задает архитектуру для создания кода на платформе x64. См. также: [/Arch (x86)](arch-x86.md) и [/Arch (ARM)](arch-arm.md).

## <a name="syntax"></a>Синтаксис

```
/arch:[AVX|AVX2|AVX512]
```

## <a name="arguments"></a>Аргументы

**/Arch: AVX**<br/>
Позволяет использовать инструкции Intel AVX.

**/Arch: AVX2**<br/>
Позволяет использовать инструкции Intel AVX 2.

**/Arch: AVX512**<br/>
Включает использование инструкций Intel Advanced Vector Extensions 512.

## <a name="remarks"></a>Комментарии

Параметр **/Arch** позволяет использовать определенные расширения набора инструкций, особенно для векторного вычисления, доступного в процессорах от Intel и AMD. Как правило, более новые процессоры могут поддерживать дополнительные расширения по сравнению с более старыми процессорами, хотя вы должны обратиться к документации по конкретному процессору или протестировать поддержку расширения набора инструкций с помощью [__cpuid](../../intrinsics/cpuid-cpuidex.md) перед выполнением кода с помощью расширения набора инструкций.

**/Arch** влияет только на создание кода для собственных функций. При использовании [параметра/clr](clr-common-language-runtime-compilation.md) для компиляции **/Arch** не влияет на создание кода для управляемых функций.

Расширения процессора имеют следующие характеристики.

- Режим по умолчанию использует инструкции SSE2 для скалярных вычислений с плавающей запятой и вектора. Эти инструкции позволяют выполнять вычисления с помощью 128-разрядных векторов целочисленных значений с одинарной точностью, двойной точностью и 1, 2, 4 или 8 байт, а также скалярных значений с плавающей запятой одиночной точности и двойной точности.

- **AVX** представил альтернативную кодировку для векторных и скалярных инструкций с плавающей запятой, которая допускает векторы 128 бит или 256 бит, а также нулевое расширение всех векторных результатов до полного размера вектора. (Для совместимости с предыдущими версиями в случае с векторными инструкциями в формате SSE сохраняются все биты, кроме бита 127.) Большинство операций с плавающей запятой расширены до 256 бит.

- **AVX2** расширяет большинство целочисленных операций до 256-разрядных векторов и позволяет использовать инструкции с предохранителем Multiply-Add (FMA).

- **AVX-512** представил еще одну форму кодирования инструкций, которая позволяет создавать 512-битные векторы, а также некоторые другие дополнительные функции. Также были добавлены инструкции для дополнительных операций.

Каждый параметр **/Arch** может также включать использование других невекторных инструкций, связанных с этим параметром. Примером является использование определенных инструкций БМИ при указании параметра **/arch: AVX2** .

`__AVX__`Символ препроцессора определяется при указании параметра компилятора **/arch: AVX**, **/arch: AVX2** или **/arch: AVX512** . `__AVX2__`Символ препроцессора определяется при указании параметра компилятора **/arch: AVX2** или **/arch: AVX512** . `__AVX512F__` `__AVX512CD__` `__AVX512BW__` `__AVX512DQ__` `__AVX512VL__` Символы препроцессора,, и определяются при указании параметра компилятора **/arch: AVX512** . Для получения дополнительной информации см. [Predefined Macros](../../preprocessor/predefined-macros.md). Параметр **/arch: AVX2** появился в Visual Studio 2013 обновление 2, версия 12.0.34567.1. Ограниченная поддержка **/arch: AVX512** была добавлена в visual Studio 2017 и развернута в visual Studio 2019.

### <a name="to-set-the-archavx-archavx2-or-archavx512-compiler-option-in-visual-studio"></a>Установка параметра компилятора/arch: AVX,/Arch: AVX2 или/Arch: AVX512 в Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md).

1. Выберите папку **Свойства конфигурации**, **C/C++** .

1. Выберите страницу свойств **Создание кода** .

1. В раскрывающемся списке **включить расширенный набор инструкций** выберите **Расширенные векторные расширения (/Arch: AVX)**, **Расширенные векторные расширения 2 (/Arch: AVX2)** или **Дополнительные векторные расширения 512 (/Arch: AVX512)**.

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.EnableEnhancedInstructionSet%2A>.

## <a name="see-also"></a>См. также раздел

[/Arch (минимальная архитектура ЦП)](arch-minimum-cpu-architecture.md)<br/>
[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)
