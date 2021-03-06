---
title: Структура файлов VCXPROJ и PROPS
description: Как в собственных файлах проекта MSBuild в C++ System. vcxproj и. props хранятся сведения о проекте.
ms.date: 09/30/2020
helpviewer_keywords:
- .vcxproj file structure
ms.assetid: 14d0c552-29db-480e-80c1-7ea89d6d8e9c
ms.openlocfilehash: 562ef0c1b371d7212f31da1917d19c012e4cbb24
ms.sourcegitcommit: f7fbdc39d73e1fb3793c396fccf7a1602af7248b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662286"
---
# <a name="vcxproj-and-props-file-structure"></a>`.vcxproj` и `.props` Структура файлов

[MSBuild](../msbuild-visual-cpp.md) — это система проектов по умолчанию в Visual Studio; При выборе **файла**  >  **создать проект** в Visual C++ создается проект MSBuild, параметры которого хранятся в файле проекта XML с расширением *`.vcxproj`* . Файл проекта также может импортировать *`.props`* файлы и *`.targets`* файлы, где можно хранить параметры.

Рекомендуется создавать и изменять *`.vcxproj`* проекты в интегрированной среде разработки и избегать ручного редактирования как можно быстрее. В большинстве случаев не нужно вручную изменять файл проекта. При возможности для изменения параметров проекта следует использовать страницы свойств Visual Studio. Подробнее см. в статье [Настройка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md).

Если вам нужны невероятные настройки в интегрированной среде разработки, рекомендуется добавить пользовательские свойства или целевые объекты. Удобными места для вставки настроек являются *`Directory.Build.props`* файлы и *`Directory.Build.targets`* , которые автоматически импортируются во все проекты на основе MSBuild.

В некоторых случаях может потребоваться *`.vcxproj`* вручную изменить файл проекта или страницу свойств. Не рекомендуется изменять его вручную, если у вас нет хорошего понимания MSBuild и следуйте указаниям в этой статье. Чтобы интегрированная среда разработки загружала и *`.vcxproj`* автоматически обновлять файлы, эти файлы имеют несколько ограничений, которые не применяются к другим файлам проекта MSBuild. Они не предназначались для редактирования вручную. Ошибки могут привести к сбою интегрированной среды разработки или к непредвиденным последствиям.

Для сценариев редактирования вручную в этой статье содержатся основные сведения о структуре *`.vcxproj`* и связанных файлах.

**Внимание!**

Если вы решили изменить *`.vcxproj`* файл вручную, учитывайте следующие факты.

- Структура файла должна соответствовать предписанной форме, которая описана в этой статье.

- В настоящее время система проектов Visual Studio C++ не поддерживает подстановочные знаки и списки непосредственно в элементах проекта. Например, эти формы не поддерживаются:

   ```xml
   <ItemGroup>
     <None Include="*.txt"/>
     <ClCompile Include="a.cpp;b.cpp"/>
   </ItemGroup>
   ```

   Дополнительные сведения о поддержке подстановочных знаков в проектах и возможных обходных путях см. в разделе [ `.vcxproj` файлы и подстановочные знаки](vcxproj-files-and-wildcards.md).

- В настоящее время система проектов Visual Studio C++ не поддерживает макросы в путях к элементам проекта. Например, эта форма не поддерживается:

   ```xml
   <ItemGroup>
     <ClCompile Include="$(IntDir)\generated.cpp"/>
   </ItemGroup>
   ```

   "Не поддерживается" означает, что макросы не будут гарантированно работать для всех операций в интегрированной среде разработки. Макросы, которые не изменяют свое значение в различных конфигурациях, должны работать, но могут не сохраняться при перемещении элемента в другой фильтр или проект. Макросы, изменяющие их значения для различных конфигураций, приведут к проблемам. Это обусловлено тем, что интегрированная среда разработки не ожидает, что пути к элементам проекта различаются для разных конфигураций проекта.

- Для правильного добавления, удаления или изменения свойств проекта при их изменении в диалоговом окне **свойств проекта** файл должен содержать отдельные группы для каждой конфигурации проекта. Условия должны быть в следующей форме:

   ```xml
   Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'"
   ```

- Каждое свойство должно быть указано в группе с правильной меткой, как указано в файле правила свойств. Дополнительные сведения см. в разделе [XML-файлы правил для страниц свойств](property-page-xml-files.md).

## <a name="vcxproj-file-elements"></a>`.vcxproj` элементы File

Просмотреть содержимое файла можно в *`.vcxproj`* любом текстовом или XML-редакторе. Просмотреть можно и в Visual Studio, щелкнув проект в обозревателе решений, выбрав **Выгрузить проект** и затем **Изменить Foo.vcxproj**.

Первое, на что нужно обратить внимание, — это определенный порядок следования элементов верхнего уровня. Пример:

- Большинство групп свойств и групп определений элементов расположено после импорта для Microsoft.Cpp.Default.props.

- Все целевые объекты импортируются в конце файла.

- Существует несколько групп свойств, каждая из которых имеет уникальную метку, и все они расположены в определенном порядке.

Порядок элементов в файле проекта жизненно важен, поскольку MSBuild основан на модели последовательной оценки.  Если файл проекта, включая все импортированные *`.props`* файлы и *`.targets`* , состоит из нескольких определений свойства, Последнее определение переопределяет предыдущие. В следующем примере значение "XYZ" будет задано во время компиляции, так как модуль MSBUild встречает его в последний раз во время его оценки.

```xml
  <MyProperty>abc</MyProperty>
  <MyProperty>xyz</MyProperty>
```

В следующем фрагменте кода показан минимальный *`.vcxproj`* файл. Все *`.vcxproj`* файлы, создаваемые Visual Studio, будут содержать эти элементы MSBuild верхнего уровня. Они будут отображаться в этом порядке, хотя они могут содержать несколько копий каждого такого элемента верхнего уровня. Все `Label` атрибуты являются произвольными тегами, которые используются только в Visual Studio как сигнпостс для редактирования; они не имеют других функций.

```xml
<Project DefaultTargets="Build" ToolsVersion="4.0" xmlns='http://schemas.microsoft.com/developer/msbuild/2003'>
  <ItemGroup Label="ProjectConfigurations" />
  <PropertyGroup Label="Globals" />
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.default.props" />
  <PropertyGroup Label="Configuration" />
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
  <ImportGroup Label="ExtensionSettings" />
  <ImportGroup Label="PropertySheets" />
  <PropertyGroup Label="UserMacros" />
  <PropertyGroup />
  <ItemDefinitionGroup />
  <ItemGroup />
  <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
  <ImportGroup Label="ExtensionTargets" />
</Project>
```

В следующих разделах описывается назначение каждого из этих элементов и порядок их упорядочивания:

### <a name="project-element"></a>Элемент Project

```xml
<Project DefaultTargets="Build" ToolsVersion="4.0" xmlns='http://schemas.microsoft.com/developer/msbuild/2003' >
```

`Project` является корневым узлом. Он указывает используемую версию MSBuild, а также целевой объект по умолчанию для выполнения при передаче этого файла в MSBuild.exe.

### <a name="projectconfigurations-itemgroup-element"></a>Элемент ProjectConfigurations ItemGroup

```xml
<ItemGroup Label="ProjectConfigurations" />
```

`ProjectConfigurations` содержит описание конфигурации проекта. В качестве примера можно привести Debug|Win32, Release|Win32, Debug|ARM и т. д. Многие параметры проекта относятся к конкретной конфигурации. Например, вы, вероятно, захотите задать свойства оптимизации для сборки выпуска, но не для отладочной сборки.

`ProjectConfigurations`Группа элементов не используется во время сборки. Интегрированная среда разработки Visual Studio требует, чтобы она загружала проект. Эту группу элементов можно переместить в *`.props`* файл и импортировать в *`.vcxproj`* файл. Однако в этом случае, если необходимо добавить или удалить конфигурации, необходимо вручную изменить *`.props`* файл; вы не сможете использовать интегрированную среду разработки.

### <a name="projectconfiguration-elements"></a>Элементы ProjectConfiguration

В следующем фрагменте кода показана конфигурация проекта. В этом примере в качестве имени конфигурации используется "Debug | x64". Имя конфигурации проекта должно быть в формате `$(Configuration)|$(Platform)` . `ProjectConfiguration`Узел может иметь два свойства: `Configuration` и `Platform` . Эти свойства задаются автоматически значениями, указанными здесь, когда конфигурация активна.

```xml
<ProjectConfiguration Include="Debug|x64">
  <Configuration>Debug</Configuration>
  <Platform>x64</Platform>
</ProjectConfiguration>
```

В интегрированной среде разработки требуется найти конфигурацию проекта для любого сочетания `Configuration` значений и, `Platform` используемых во всех `ProjectConfiguration` элементах. Часто это означает, что проект может иметь бессмысленные конфигурации проекта для выполнения этого требования. Например, если проект имеет следующие конфигурации:

- Debug|Win32;

- Retail|Win32;

- Special 32-bit Optimization|Win32;

то он должен содержать и следующие конфигурации, хотя конфигурация Special 32-bit Optimization не имеет смысла для x64:

- Отладка|x64

- Retail|x64;

- Special 32-bit Optimization|x64.

Вы можете отключить команды сборки и развертывания для любой конфигурации в **диспетчере конфигурации решения**.

### <a name="globals-propertygroup-element"></a>Элемент Globals PropertyGroup

```xml
<PropertyGroup Label="Globals" />
```

`Globals` содержит параметры уровня проекта, такие как `ProjectGuid` , `RootNamespace` , и `ApplicationType` или `ApplicationTypeRevision` . Последние два часто определяют целевую ОС. Проект может ориентироваться только на одну ОС, поскольку в настоящее время ссылки и элементы проекта не могут иметь условий. Эти свойства обычно не переопределяются в другом месте в файле проекта. Эта группа не зависит от конфигурации, и обычно `Globals` в файле проекта существует только одна группа.

### <a name="microsoftcppdefaultprops-import-element"></a>Элемент Microsoft.Cpp.default.props Import

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.default.props" />
```

Страница свойств **Microsoft. cpp. Default. props** поставляется с Visual Studio и не может быть изменена. Она содержит параметры по умолчанию для проекта. Эти значения по умолчанию могут различаться в зависимости от ApplicationType.

### <a name="configuration-propertygroup-elements"></a>Элементы Configuration PropertyGroup

```xml
<PropertyGroup Label="Configuration" />
```

Группа свойств `Configuration` имеет прикрепленное условие конфигурации (например, `Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'"`) и представлена несколькими копиями — по одной на конфигурации. Эта группа свойств содержит свойства, заданные для конкретной конфигурации. Свойства конфигурации включают PlatformToolset и управляют включением системных страниц свойств в **Microsoft.Cpp.props**. Например, если определено свойство `<CharacterSet>Unicode</CharacterSet>`, то системная страница свойств **microsoft.Cpp.unicodesupport.props** будет включена. При проверке **Microsoft. cpp. props**вы увидите строку: `<Import Condition="'$(CharacterSet)' == 'Unicode'" Project="$(VCTargetsPath)\microsoft.Cpp.unicodesupport.props" />` .

### <a name="microsoftcppprops-import-element"></a>Элемент Microsoft.Cpp.props Import

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
```

Страница свойств **Microsoft. cpp. props** (напрямую или через импорт) определяет значения по умолчанию для многих свойств конкретного инструмента. К примерам относятся свойства оптимизации компилятора и уровня предупреждения, свойство Типелибраринаме средства MIDL и т. д. Он также импортирует различные системные таблицы свойств в зависимости от того, какие свойства конфигурации определены в группе свойств непосредственно перед ней.

### <a name="extensionsettings-importgroup-element"></a>Элемент ExtensionSettings ImportGroup

```xml
<ImportGroup Label="ExtensionSettings" />
```

Группа `ExtensionSettings` содержит операции импорта для страниц свойств, входящих в настройки сборки. Настройка сборки определяется до трех файлов: *`.targets`* файла, *`.props`* файла и *`.xml`* файла. Эта группа импорта содержит импорты для *`.props`* файла.

### <a name="propertysheets-importgroup-elements"></a>Элемент PropertySheets ImportGroup

```xml
<ImportGroup Label="PropertySheets" />
```

Группа `PropertySheets` содержит операции импорта для страниц свойств. Эти импорты являются страницами свойств, которые добавляются с помощью представления диспетчер свойств в Visual Studio. Порядок, в котором указаны эти операции импорта, имеет значение и отражен в диспетчере свойств. Обычно файл проекта содержит несколько экземпляров этого типа группы импорта, по одному для каждой конфигурации проекта.

### <a name="usermacros-propertygroup-element"></a>Элемент UserMacros PropertyGroup

```xml
<PropertyGroup Label="UserMacros" />
```

`UserMacros` содержит свойства, создаваемые в качестве переменных, которые используются для настройки процесса сборки. Например, можно определить пользовательский макрос для задания настраиваемого пути выходных данных как $(CustomOutputPath) и использовать его для определения других переменных. Эта группа свойств содержит такие свойства. В Visual Studio эта группа не заполняется в файле проекта, так как Visual C++ не поддерживает пользовательские макросы для конфигураций. Пользовательские макросы поддерживаются на страницах свойств.

### <a name="per-configuration-propertygroup-elements"></a>Элементы PropertyGroup для отдельных конфигураций

```xml
<PropertyGroup />
```

Существует несколько экземпляров этой группы свойств, по одному на конфигурацию для всех конфигураций проекта. Каждая группа свойств должна иметь одно прикрепленное условие конфигурации. Если отсутствуют какие-либо конфигурации, диалоговое окно **Свойства проекта** будет работать неправильно. В отличие от групп свойств, перечисленных ранее, она не имеет метки. Она содержит параметры на уровне конфигурации проекта. Эти параметры применяются ко всем файлам, входящим в указанную группу элементов. Здесь происходит инициализация метаданных для определения элемента настройки сборки.

Эти PropertyGroup должны следовать после `<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />` и не должны иметь других PropertyGroup без метки перед ним (в противном случае редактирование свойств проекта не будет работать правильно).

### <a name="per-configuration-itemdefinitiongroup-elements"></a>Элементы ItemDefinitionGroup для отдельных конфигураций

```xml
<ItemDefinitionGroup />
```

Содержит определения элемента. Эти определения должны следовать тем же правилам, что и элементы конфигурации без метки `PropertyGroup` .

### <a name="itemgroup-elements"></a>Элементы ItemGroup

```xml
<ItemGroup />
```

`ItemGroup` элементы содержат элементы (исходные файлы и т. д.) в проекте. Условия не поддерживаются для элементов проекта (т. е. типов элементов, которые обрабатываются как элементы проекта по определениям правил).

Метаданные должны иметь условия конфигурации для каждой конфигурации, даже если они все одинаковы. Пример:

```xml
<ItemGroup>
  <ClCompile Include="stdafx.cpp">
    <TreatWarningAsError Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">true</TreatWarningAsError>
    <TreatWarningAsError Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">true</TreatWarningAsError>
  </ClCompile>
</ItemGroup>
```

В настоящее время система проектов Visual Studio C++ не поддерживает подстановочные знаки в элементах проекта.

```xml
<ItemGroup>
  <ClCompile Include="*.cpp"> <!--Error-->
</ItemGroup>
```

В настоящее время система проектов Visual Studio C++ не поддерживает макросы в элементах проекта.

```xml
<ItemGroup>
  <ClCompile Include="$(IntDir)\generated.cpp"> <!--not guaranteed to work in all scenarios-->
</ItemGroup>
```

Ссылки указываются в ItemGroup и имеют следующие ограничения:

- Ссылки не поддерживают условия.

- Метаданные ссылок не поддерживают условия.

### <a name="microsoftcpptargets-import-element"></a>Элемент Microsoft.Cpp.targets Import

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

Определяет (напрямую или с помощью импорта) целевые объекты C++, такие как сборка, очистка и т. д.

### <a name="extensiontargets-importgroup-element"></a>Элемент ExtensionTargets ImportGroup

```xml
<ImportGroup Label="ExtensionTargets" />
```

Эта группа содержит операции импорта для целевых файлов настройки сборки.

## <a name="impact-of-incorrect-ordering"></a>Влияние неправильного порядка

Интегрированная среда разработки Visual Studio зависит от файла проекта с упорядочением, описанным выше. Например, при определении значения свойства на страницах свойств интегрированная среда разработки обычно помещает определение свойства в группу свойств с пустой меткой. Такой порядок гарантирует, что значения по умолчанию, указанные на страницах системных свойств, переопределяются определяемыми пользователем значениями. Точно так же целевые файлы импортируются в конце, так как они используют свойства, определенные ранее, и так как они обычно не определяют сами свойства. Аналогичным образом страницы свойств пользователя импортируются после системных вкладок свойств (входящих в *`Microsoft.Cpp.props`* ). Этот порядок гарантирует, что пользователь может переопределить любые значения по умолчанию, которые были добавлены на системные вкладки свойств.

Если *`.vcxproj`* файл не соответствует этому макету, результаты сборки могут отличаться от предполагаемых. Например, если вы по ошибке импортировали страницу системных свойств после страниц свойств, определенных пользователем, то параметры пользователя будут переопределены на страницах системных свойств.

Даже время разработки интегрированной среды разработки зависит от некоторого экстента по правильному упорядочению элементов. Например, если в *`.vcxproj`* файле нет `PropertySheets` группы импорта, интегрированная среда разработки может не определить место размещения новой страницы свойств, созданной пользователем в **Диспетчер свойств**. Это может привести к переопределению пользовательского листа на системном листе. Хотя эвристический подход, используемый интегрированной средой разработки, может допускать незначительные несоответствия в *`.vcxproj`* структуре файлов, настоятельно рекомендуется не отклоняться от структуры, приведенной ранее в этой статье.

## <a name="how-the-ide-uses-element-labels"></a>Использование меток элемента интегрированной средой разработки

В интегрированной среде разработки при установке свойства **усеофатл** на странице свойств Общие оно записывается в группу свойств конфигурации в файле проекта. Свойство **TargetName** на той же странице свойств записывается в группу свойств без метки для каждой конфигурации. Visual Studio ищет в XML-файле страницы свойств сведения о том, куда нужно записать каждое свойство. Если на странице свойств **Общие** есть английская версия Visual Studio 2019 Enterprise Edition, то этот файл имеет значение `%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\VC\VCTargets\1033\general.xml` . XML-файл правил страницы свойств определяет статические данные о правиле и всех его свойствах. В эти данные входит предпочтительное положение свойства правила в конечном файле (файл, куда будет записано его значение). Предпочтительное положение задается атрибутом Label в элементах файла проекта.

## <a name="property-sheet-layout"></a>Макет страницы свойств

В следующем фрагменте XML-кода приведен минимальный макет файла (PROPS) страницы свойств. Он похож на *`.vcxproj`* файл, и функциональность *`.props`* элементов можно вывести из предыдущего обсуждения.

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ImportGroup Label="PropertySheets" />
  <PropertyGroup Label="UserMacros" />
  <PropertyGroup />
  <ItemDefinitionGroup />
  <ItemGroup />
</Project>
```

Чтобы создать собственную страницу свойств, скопируйте один из *`.props`* файлов в *`VCTargets`* папке и измените его в целях. Для Visual Studio 2019 Enterprise Edition по умолчанию *`VCTargets`* используется путь `%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\VC\VCTargets` .

## <a name="see-also"></a>См. также раздел

[Установка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md)\
[XML-файлы страницы свойств](property-page-xml-files.md)\
[`.vcxproj` файлы и подстановочные знаки](vcxproj-files-and-wildcards.md)
