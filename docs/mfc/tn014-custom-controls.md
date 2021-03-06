---
description: 'Дополнительные сведения о: TN014: пользовательские элементы управления'
title: TN014. Пользовательские элементы управления
ms.date: 06/28/2018
f1_keywords:
- vc.controls
helpviewer_keywords:
- TN014
- custom controls [MFC]
ms.assetid: 1917a498-f643-457c-b570-9a0af7dbf7bb
ms.openlocfilehash: c9b069e0101b279558c5bcd4ffb7f457120e8187
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97215980"
---
# <a name="tn014-custom-controls"></a>TN014. Пользовательские элементы управления

В этом заметке описывается поддержка MFC для пользовательских элементов управления и самостоятельного рисования. Он также описывает динамическое подклассы и описывает связь между объектами [CWnd](../mfc/reference/cwnd-class.md) и `HWND` s.

В образце примера приложения MFC показано, как использовать множество пользовательских элементов управления. См. исходный код для общего примера [CTRLTEST](../overview/visual-cpp-samples.md) в MFC и Справка в Интернете.

## <a name="owner-draw-controlsmenus"></a>Owner-Drawные элементы управления и меню

Windows обеспечивает поддержку рисуемых владельцем элементов управления и меню с помощью сообщений Windows. Родительское окно любого элемента управления или меню получает эти сообщения и вызывает функции в ответе. Эти функции можно переопределить для настройки внешнего вида и поведения элемента управления или меню, рисуемого владельцем.

MFC напрямую поддерживает прорисовку владельцем с помощью следующих функций:

- [CWnd::OnDrawItem](../mfc/reference/cwnd-class.md#ondrawitem)

- [CWnd::OnMeasureItem](../mfc/reference/cwnd-class.md#onmeasureitem)

- [CWnd::OnCompareItem](../mfc/reference/cwnd-class.md#oncompareitem)

- [CWnd::OnDeleteItem](../mfc/reference/cwnd-class.md#ondeleteitem)

Эти функции можно переопределить в `CWnd` производном классе, чтобы реализовать пользовательское поведение рисования.

Этот подход не приводит к повторному использованию кода. При наличии двух аналогичных элементов управления в двух разных `CWnd` классах необходимо реализовать поведение пользовательского элемента управления в двух местах. Эта проблема решается с помощью архитектуры собственного элемента управления, поддерживаемой MFC.

## <a name="self-draw-controls-and-menus"></a>Self-Draw элементы управления и меню

MFC предоставляет реализацию по умолчанию (в `CWnd` классах и [кмену](../mfc/reference/cmenu-class.md) ) для стандартных сообщений, рисуемых владельцем. В этой реализации по умолчанию будут декодированы параметры рисования владельцем и делегированы сообщения, рисуемые владельцем, в элементы управления или меню. Это называется самостоятельным рисованием, поскольку код рисования находится в классе элемента управления или меню, а не в окне владельца.

Используя собственные элементы управления, можно создавать многократно используемые классы элементов управления, которые используют семантику рисования владельцем для отображения элемента управления. Код для рисования элемента управления находится в классе Control, а не в его родителе. Это объектно-ориентированный подход к программированию пользовательских элементов управления. Добавьте следующий список функций в самостоятельные классы:

- Для самостоятельного отображения кнопок:

    ```cpp
    CButton:DrawItem(LPDRAWITEMSTRUCT);
    // insert code to draw this button
    ```

- Для самостоятельного отображения меню:

    ```cpp
    CMenu:MeasureItem(LPMEASUREITEMSTRUCT);
    // insert code to measure the size of an item in this menu
    CMenu:DrawItem(LPDRAWITEMSTRUCT);
    // insert code to draw an item in this menu
    ```

- Для саморисуемых списков:

    ```cpp
    CListBox:MeasureItem(LPMEASUREITEMSTRUCT);
    // insert code to measure the size of an item in this list box
    CListBox:DrawItem(LPDRAWITEMSTRUCT);
    // insert code to draw an item in this list box

    CListBox:CompareItem(LPCOMPAREITEMSTRUCT);
    // insert code to compare two items in this list box if LBS_SORT
    CListBox:DeleteItem(LPDELETEITEMSTRUCT);
    // insert code to delete an item from this list box
    ```

- Для саморисуемых полей со списком:

    ```cpp
    CComboBox:MeasureItem(LPMEASUREITEMSTRUCT);
    // insert code to measure the size of an item in this combo box
    CComboBox:DrawItem(LPDRAWITEMSTRUCT);
    // insert code to draw an item in this combo box

    CComboBox:CompareItem(LPCOMPAREITEMSTRUCT);
    // insert code to compare two items in this combo box if CBS_SORT
    CComboBox:DeleteItem(LPDELETEITEMSTRUCT);
    // insert code to delete an item from this combo box
    ```

Дополнительные сведения о структурах, рисуемых владельцем ([дравитемструкт](/windows/win32/api/winuser/ns-winuser-drawitemstruct), [меасуреитемструкт](/windows/win32/api/winuser/ns-winuser-measureitemstruct), [COMPAREITEMSTRUCT](/windows/win32/api/winuser/ns-winuser-compareitemstruct)и [делетеитемструкт](/windows/win32/api/winuser/ns-winuser-deleteitemstruct)), см. в документации по MFC для `CWnd::OnDrawItem` ,, `CWnd::OnMeasureItem` `CWnd::OnCompareItem` и `CWnd::OnDeleteItem` соответственно.

## <a name="using-self-draw-controls-and-menus"></a>Использование самостоятельно рисуемых элементов управления и меню

Для меню с самостоятельным выводом необходимо переопределить `OnMeasureItem` `OnDrawItem` методы и.

Для самостоятельных списков и полей со списками необходимо переопределить `OnMeasureItem` и `OnDrawItem` . Для полей со списками в шаблоне диалогового окна необходимо указать LBS_OWNERDRAWVARIABLE стиль для списков или стиль CBS_OWNERDRAWVARIABLE. Стиль ОВНЕРДРАВФИКСЕД не будет работать с саморисуемыми элементами, так как фиксированная высота элемента определяется до присоединения к списку элементов управления для самоотрисовки. (Для преодоления этого ограничения можно использовать методы [CListBox:: сетитемхеигхт](../mfc/reference/clistbox-class.md#setitemheight) и [CComboBox:: сетитемхеигхт](../mfc/reference/ccombobox-class.md#setitemheight) .)

При переключении на стиль ОВНЕРДРАВВАРИАБЛЕ система будет принудительно применять стиль НОИНТЕГРАЛХЕИГХТ к элементу управления. Поскольку элемент управления не может вычислить целочисленную высоту с элементами изменяемого размера, стиль по умолчанию ИНТЕГРАЛХЕИГХТ игнорируется, а элемент управления всегда НОИНТЕГРАЛХЕИГХТ. Если элементы имеют фиксированную высоту, можно предотвратить прорисовку частичных элементов, указав размер элемента управления равным целочисленному множителю размера элемента.

Для списков саморисовок и полей со списком, имеющих LBS_SORT или CBS_SORT стиль, необходимо переопределить `OnCompareItem` метод.

Для списков и полей со списками саморисования `OnDeleteItem` обычно не переопределяется. Можно переопределить, `OnDeleteItem` Если требуется выполнить специальную обработку. Один из случаев, когда это может быть применимо, — при хранении дополнительной памяти или других ресурсов с каждым полем списка или элементом поля со списком.

## <a name="examples-of-self-drawing-controls-and-menus"></a>Примеры элементов управления Self-Drawing и меню

В образце библиотеки MFC "общий пример [" представлена](../overview/visual-cpp-samples.md) выборка для самостоятельного меню и саморисуемого списка.

Наиболее типичным примером кнопки саморисования является растровая кнопка. Кнопка с точечным рисунком — это кнопка, которая показывает одно, два или три растровые изображения для различных состояний. Пример приведен в классе MFC [кбитмапбуттон](../mfc/reference/cbitmapbutton-class.md).

## <a name="dynamic-subclassing"></a>Динамические подклассы

Иногда может потребоваться изменить функциональность уже существующего объекта. В предыдущих примерах требовалось настроить элементы управления до их создания. Динамическое создание подклассов позволяет настроить уже созданный элемент управления.

Подклассы — это термин Windows для замены <xref:System.Windows.Forms.Control.WndProc%2A> окна настраиваемым `WndProc` и вызовом старого набора `WndProc` функций по умолчанию.

Это не следует путать с производностью класса C++. Для уточнения, *базовый класс* терминов C++ и *производный класс* аналогичны *суперклассу* и *подклассу* в объектной модели Windows. Наследование C++ с помощью MFC и подкласса Windows функционально аналогично, за исключением того, что C++ не поддерживает динамическое подклассы.

`CWnd`Класс предоставляет соединение между объектом C++ (производным от `CWnd` ) и объектом окна Windows (называемым `HWND` ).

Существуют три распространенных способа их применения.

- `CWnd` создает `HWND` . Поведение можно изменить в производном классе, создав класс, производный от `CWnd` . `HWND`Создается, когда приложение вызывает метод [CWnd:: Create](../mfc/reference/cwnd-class.md#create).

- Приложение присоединяет `CWnd` к существующему `HWND` . Поведение существующего окна не изменяется. Это случай делегирования, и это можно сделать, вызвав [CWnd:: Attach](../mfc/reference/cwnd-class.md#attach) для псевдонима существующего `HWND` `CWnd` объекта.

- `CWnd` прикрепляется к существующему `HWND` и может изменить поведение в производном классе. Это называется динамическим подклассом, так как мы изменим поведение, а значит, класс объекта Windows во время выполнения.

Реализовать динамическое подклассы можно с помощью методов [CWnd:: субклассвиндов](../mfc/reference/cwnd-class.md#subclasswindow) и[CWnd:: субклассдлгитем](../mfc/reference/cwnd-class.md#subclassdlgitem).

Обе подпрограммы присоединяются `CWnd` к существующему объекту `HWND` . `SubclassWindow` принимает `HWND` непосредственно. `SubclassDlgItem` — Это вспомогательная функция, которая принимает идентификатор элемента управления и родительское окно. `SubclassDlgItem` предназначен для присоединения объектов C++ к элементам управления диалогового окна, созданным из шаблона диалогового окна.

Несколько примеров использования и см. в примере с [образцом CTRLTEST](../overview/visual-cpp-samples.md) `SubclassWindow` `SubclassDlgItem` .

## <a name="see-also"></a>См. также раздел

[Технические примечания по номеру](../mfc/technical-notes-by-number.md)<br/>
[Технические примечания по категориям](../mfc/technical-notes-by-category.md)
