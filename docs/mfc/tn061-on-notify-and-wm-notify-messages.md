---
description: 'Дополнительные сведения о: TN061: ON_NOTIFY и WM_NOTIFY сообщения'
title: TN061. Сообщения ON_NOTIFY и WM_NOTIFY
ms.date: 06/28/2018
helpviewer_keywords:
- ON_NOTIFY_EX message [MFC]
- TN061
- ON_NOTIFY message [MFC]
- ON_NOTIFY_EX_RANGE message [MFC]
- ON_NOTIFY_RANGE message [MFC]
- notification messages
- WM_NOTIFY message
ms.assetid: 04a96dde-7049-41df-9954-ad7bb5587caf
ms.openlocfilehash: ecbbc03ad7328b163f89e5b1da095c8c179df097
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97214758"
---
# <a name="tn061-on_notify-and-wm_notify-messages"></a>TN061. Сообщения ON_NOTIFY и WM_NOTIFY

> [!NOTE]
> Следующее техническое примечание не было обновлено, поскольку сначала оно было включено в электронную документацию. В результате некоторые процедуры и разделы могут быть устаревшими или неверными. Для получения последних сведений рекомендуется выполнить поиск интересующей темы в алфавитном указателе документации в Интернете.

В этом техническом примечании содержатся общие сведения о новом WM_NOTIFY сообщении и описание рекомендуемого (и наиболее распространенного) способа обработки сообщений WM_NOTIFY в приложении MFC.

**Сообщения уведомления в Windows 3. x**

В Windows 3. x элементы управления уведомляют свои родительские события, такие как щелчки мыши, изменения в содержимом и выделении, а также управляют фоновым рисованием, отправляя сообщение родительскому элементу. Простые уведомления отправляются в виде специальных сообщений WM_COMMAND с кодом уведомления (например, BN_CLICKED) и ИДЕНТИФИКАТОРом управления, упакованным в *wParam* , и маркером элемента управления в *lParam*. Обратите внимание, что, поскольку *wParam* и *lParam* заполнены, не существует способа передачи дополнительных данных — эти сообщения могут быть только простыми уведомлениями. Например, в уведомлении BN_CLICKED не существует способа отправки сведений о расположении курсора мыши при нажатии кнопки.

Когда элементы управления в Windows 3. x должны отправить сообщение с уведомлением, которое содержит дополнительные данные, они используют разнообразные специальные сообщения, в том числе WM_CTLCOLOR, WM_VSCROLL, WM_HSCROLL, WM_DRAWITEM, WM_MEASUREITEM, WM_COMPAREITEM, WM_DELETEITEM, WM_CHARTOITEM, WM_VKEYTOITEM и т. д. Эти сообщения могут быть отражены обратно в элемент управления, который их отправил. Дополнительные сведения см. в разделе [TN062: отражение сообщения для элементов управления Windows](../mfc/tn062-message-reflection-for-windows-controls.md).

**Сообщения уведомлений в Win32**

Для элементов управления, которые существовали в Windows 3,1, API Win32 использует большинство сообщений уведомлений, которые использовались в Windows 3. x. Однако Win32 также добавляет ряд сложных, сложных элементов управления в те, которые поддерживаются в Windows 3. x. Часто эти элементы управления должны передавать дополнительные данные с их сообщениями уведомления. Вместо добавления нового сообщения **WM_** <strong>\*</strong> для каждого нового уведомления, требующего дополнительных данных, конструкторы API Win32 решили добавить только одно сообщение, WM_NOTIFY, которое может передавать любой объем дополнительных данных в стандартизованном виде.

WM_NOTIFY сообщения содержат идентификатор элемента управления, отправляющего сообщение в параметре *wParam* , и указатель на структуру в *lParam*. Эта структура является либо структурой **NMHDR** , либо некоторой крупной структурой, которая имеет структуру **NMHDR** в качестве первого элемента. Обратите внимание, что поскольку элемент **NMHDR** является первым, указатель на эту структуру можно использовать как указатель на **NMHDR** или как указатель на более крупную структуру в зависимости от способа приведения.

В большинстве случаев указатель будет указывать на большую структуру, и при ее использовании его необходимо привести. Только в нескольких уведомлениях, таких как общие уведомления (имена которых начинаются с **NM_**), а TTN_SHOW и TTN_POP уведомления элемента управления всплывающей подсказки, — это структура **NMHDR** , которая фактически используется.

Структура **NMHDR** или начальный элемент содержит маркер и идентификатор элемента управления, отправляющего сообщение, и код уведомления (например, TTN_SHOW). Ниже показан формат структуры **NMHDR** .

```cpp
typedef struct tagNMHDR {
    HWND hwndFrom;
    UINT idFrom;
    UINT code;
} NMHDR;
```

Для TTN_SHOW сообщения элементу **Code** будет присвоено значение TTN_SHOW.

Большинство уведомлений передают указатель на более крупную структуру, которая содержит структуру **NMHDR** в качестве первого элемента. Например, рассмотрим структуру, используемую сообщением LVN_KEYDOWN уведомления элемента управления представления списка, которое отправляется при нажатии клавиши в элементе управления "представление списка". Указатель указывает на структуру **LV_KEYDOWN** , которая определяется, как показано ниже:

```cpp
typedef struct tagLV_KEYDOWN {
    NMHDR hdr;
    WORD wVKey;
    UINT flags;
} LV_KEYDOWN;
```

Обратите внимание, что поскольку элемент **NMHDR** сначала находится в этой структуре, указатель, который вы передали в сообщении уведомления, может быть приведен к указателю на **NMHDR** или указателю на **LV_KEYDOWN**.

**Уведомления, общие для всех новых элементов управления Windows**

Некоторые уведомления являются общими для всех новых элементов управления Windows. Эти уведомления передают указатель на структуру **NMHDR** .

|Код уведомления|Отправлено, так как|
|-----------------------|------------------|
|NM_CLICK|Пользователь щелкнул левой кнопкой мыши в элементе управления|
|NM_DBLCLK|Пользователь дважды щелкнул левую кнопку мыши в элементе управления|
|NM_RCLICK|Пользователь щелкнул правой кнопкой мыши в элементе управления|
|NM_RDBLCLK|Пользователь дважды щелкнул правой кнопкой мыши в элементе управления|
|NM_RETURN|Пользователь нажал клавишу ВВОД, когда элемент управления имеет фокус ввода|
|NM_SETFOCUS|Элементу управления передан фокус ввода|
|NM_KILLFOCUS|Элемент управления потерял фокус ввода|
|NM_OUTOFMEMORY|Элементу управления не удалось выполнить операцию из-за нехватки доступной памяти|

## <a name="on_notify-handling-wm_notify-messages-in-mfc-applications"></a><a name="_mfcnotes_on_notify.3a_.handling_wm_notify_messages_in_mfc_applications"></a> ON_NOTIFY: обработка сообщений WM_NOTIFY в приложениях MFC

Функция `CWnd::OnNotify` обрабатывает сообщения уведомления. Его реализация по умолчанию проверяет схему сообщений для вызова обработчиков уведомлений. В общем случае вы не переопределяете `OnNotify` . Вместо этого вы предоставляете функцию обработчика и добавляете запись схемы сообщений для этого обработчика в схему сообщений класса окна-владельца.

ClassWizard, используя страницу свойств ClassWizard, может создать ON_NOTIFY записи схемы сообщений и предоставить вам каркас функции обработчика. Дополнительные сведения об использовании ClassWizard для упрощения см. в разделе [сопоставление сообщений с функциями](../mfc/reference/mapping-messages-to-functions.md).

Макрос схемы сообщения ON_NOTIFY имеет следующий синтаксис:

```cpp
ON_NOTIFY(wNotifyCode, id, memberFxn)
```

Используются следующие параметры.

*wNotifyCode*<br/>
Код для обрабатываемого сообщения уведомления, например LVN_KEYDOWN.

*id*<br/>
Дочерний идентификатор элемента управления, для которого отправляется уведомление.

*мемберфксн*<br/>
Функция-член, вызываемая при отправке уведомления.

Функция члена должна быть объявлена со следующим прототипом:

```cpp
afx_msg void memberFxn(NMHDR* pNotifyStruct, LRESULT* result);
```

Используются следующие параметры.

*пнотифиструкт*<br/>
Указатель на структуру уведомления, как описано в разделе выше.

*result*<br/>
Указатель на код результата, который вы задаете перед возвратом.

## <a name="example"></a>Пример

Чтобы указать, что функция-член должна выполнять `OnKeydownList1` обработку LVN_KEYDOWN сообщений от, `CListCtrl` идентификатором которых является `IDC_LIST1` , вы должны использовать ClassWizard, чтобы добавить следующий код в схему сообщения:

```cpp
ON_NOTIFY(LVN_KEYDOWN, IDC_LIST1, OnKeydownList1)
```

В приведенном выше примере функция, предоставляемая функцией ClassWizard, имеет следующее:

```cpp
void CMessageReflectionDlg::OnKeydownList1(NMHDR* pNMHDR, LRESULT* pResult)
{
    LV_KEYDOWN* pLVKeyDow = (LV_KEYDOWN*)pNMHDR;

    // TODO: Add your control notification handler
    //       code here

    *pResult = 0;
}
```

Обратите внимание, что ClassWizard предоставляет автоматический указатель правильного типа. Доступ к структуре уведомлений можно получить с помощью *пнмхдр* или *плвкэйдов*.

## <a name="on_notify_range"></a><a name="_mfcnotes_on_notify_range"></a> ON_NOTIFY_RANGE

Если необходимо обработать одно и то же сообщение WM_NOTIFY для набора элементов управления, можно использовать ON_NOTIFY_RANGE, а не ON_NOTIFY. Например, у вас может быть набор кнопок, для которых необходимо выполнить одно и то же действие для определенного сообщения уведомления.

При использовании ON_NOTIFY_RANGE вы указываете непрерывный диапазон идентификаторов дочерних элементов, для которых будет обработано сообщение уведомления, указав начальный и конечный идентификаторы дочерних элементов диапазона.

ClassWizard не обрабатывает ON_NOTIFY_RANGE; чтобы использовать его, необходимо изменить схему сообщений самостоятельно.

Для ON_NOTIFY_RANGE используются следующие записи схемы сообщений и прототип функции:

```cpp
ON_NOTIFY_RANGE(wNotifyCode, id, idLast, memberFxn)
```

Используются следующие параметры.

*wNotifyCode*<br/>
Код для обрабатываемого сообщения уведомления, например LVN_KEYDOWN.

*id*<br/>
Первый идентификатор в непрерывном диапазоне идентификаторов.

*идласт*<br/>
Последний идентификатор в непрерывном диапазоне идентификаторов.

*мемберфксн*<br/>
Функция-член, вызываемая при отправке уведомления.

Функция члена должна быть объявлена со следующим прототипом:

```cpp
afx_msg void memberFxn(UINT id, NMHDR* pNotifyStruct, LRESULT* result);
```

Используются следующие параметры.

*id*<br/>
Дочерний идентификатор элемента управления, отправившего уведомление.

*пнотифиструкт*<br/>
Указатель на структуру уведомления, как описано выше.

*result*<br/>
Указатель на код результата, который вы задаете перед возвратом.

## <a name="on_notify_ex-on_notify_ex_range"></a><a name="_mfcnotes_tn061_on_notify_ex.2c_.on_notify_ex_range"></a> ON_NOTIFY_EX, ON_NOTIFY_EX_RANGE

Если требуется, чтобы несколько объектов в маршрутизации уведомлений обрабатывали сообщение, можно использовать ON_NOTIFY_EX (или ON_NOTIFY_EX_RANGE), а не ON_NOTIFY (или ON_NOTIFY_RANGE). Единственное различие между версией **ex** и обычной версией заключается в том, что функция-член, вызываемая для версии **ex** , возвращает **логическое** значение, указывающее, следует ли продолжать обработку сообщений. Возвращение значения **false** из этой функции позволяет обрабатывать одно и то же сообщение в нескольких объектах.

ClassWizard не обрабатывает ON_NOTIFY_EX или ON_NOTIFY_EX_RANGE; Если вы хотите использовать любой из них, необходимо изменить схему сообщений самостоятельно.

Запись схемы сообщения и прототип функции для ON_NOTIFY_EX и ON_NOTIFY_EX_RANGE приведены ниже. Для параметров используются те же значения, что и для версий без **ex** .

```cpp
ON_NOTIFY_EX(nCode, id, memberFxn)
ON_NOTIFY_EX_RANGE(wNotifyCode, id, idLast, memberFxn)
```

Прототип для обоих вышеуказанных типов одинаков:

```cpp
afx_msg BOOL memberFxn(UINT id, NMHDR* pNotifyStruct, LRESULT* result);
```

В обоих случаях *идентификатор* содержит дочерний идентификатор элемента управления, отправившего уведомление.

Функция должна возвращать **значение true** , если сообщение уведомления полностью обработано, или **false** , если другие объекты в маршрутизации команд должны иметь шанс обработать сообщение.

## <a name="see-also"></a>См. также раздел

[Технические примечания по номеру](../mfc/technical-notes-by-number.md)<br/>
[Технические примечания по категориям](../mfc/technical-notes-by-category.md)
