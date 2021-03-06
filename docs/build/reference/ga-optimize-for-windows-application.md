---
description: Дополнительные сведения о:/GA (оптимизация для приложения Windows)
title: /GA (Оптимизация для приложений Windows)
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLCompilerTool.OptimizeForWindowsApplication
- /ga
helpviewer_keywords:
- /GA compiler option [C++]
- GA compiler option [C++]
- -GA compiler option [C++]
- Optimize for Windows compiler options
ms.assetid: be97323e-15a0-4836-862c-95980b51926a
ms.openlocfilehash: f9d65dce26e80b585abc4d67e2eef55f10cb365b
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97191983"
---
# <a name="ga-optimize-for-windows-application"></a>/GA (Оптимизация для приложений Windows)

Приводит к более эффективному коду exe-файла для доступа к переменным локального хранилища потока (TLS).

## <a name="syntax"></a>Синтаксис

```
/GA
```

## <a name="remarks"></a>Remarks

**/GA** ускоряет доступ к данным, объявленным с помощью [__declspec (thread)](../../cpp/declspec.md) в программе на основе Windows. Если задан этот параметр, макрос [__tls_index](/windows/win32/ProcThread/thread-local-storage) считается равным 0.

Использование **/GA** для библиотеки DLL может привести к неправильному созданию кода.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Откройте папку **C/C++** .

1. Выберите страницу свойств **Командная строка** .

1. Введите параметр компилятора в поле **Дополнительные параметры** .

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.AdditionalOptions%2A>.

## <a name="see-also"></a>См. также раздел

[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис Command-Line компилятора КОМПИЛЯТОРОМ MSVC](compiler-command-line-syntax.md)
