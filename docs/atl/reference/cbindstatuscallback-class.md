---
description: 'Дополнительные сведения о: Кбиндстатускаллбакк Class'
title: Класс Кбиндстатускаллбакк
ms.date: 11/04/2016
f1_keywords:
- CBindStatusCallback
- ATLCTL/ATL::CBindStatusCallback
- ATLCTL/ATL::CBindStatusCallback::CBindStatusCallback
- ATLCTL/ATL::CBindStatusCallback::Download
- ATLCTL/ATL::CBindStatusCallback::GetBindInfo
- ATLCTL/ATL::CBindStatusCallback::GetPriority
- ATLCTL/ATL::CBindStatusCallback::OnDataAvailable
- ATLCTL/ATL::CBindStatusCallback::OnLowResource
- ATLCTL/ATL::CBindStatusCallback::OnObjectAvailable
- ATLCTL/ATL::CBindStatusCallback::OnProgress
- ATLCTL/ATL::CBindStatusCallback::OnStartBinding
- ATLCTL/ATL::CBindStatusCallback::OnStopBinding
- ATLCTL/ATL::CBindStatusCallback::StartAsyncDownload
- ATLCTL/ATL::CBindStatusCallback::m_dwAvailableToRead
- ATLCTL/ATL::CBindStatusCallback::m_dwTotalRead
- ATLCTL/ATL::CBindStatusCallback::m_pFunc
- ATLCTL/ATL::CBindStatusCallback::m_pT
- ATLCTL/ATL::CBindStatusCallback::m_spBindCtx
- ATLCTL/ATL::CBindStatusCallback::m_spBinding
- ATLCTL/ATL::CBindStatusCallback::m_spMoniker
- ATLCTL/ATL::CBindStatusCallback::m_spStream
helpviewer_keywords:
- asynchronous data transfer [C++]
- data transfer [C++]
- data transfer [C++], asynchronous
- CBindStatusCallback class
ms.assetid: 0f5da276-6031-4418-b2a9-a4750ef29e77
ms.openlocfilehash: 8c57328be0cb2678e671f68ac5bb44471056f457
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97146982"
---
# <a name="cbindstatuscallback-class"></a>Класс Кбиндстатускаллбакк

Этот класс реализует интерфейс `IBindStatusCallback` .

> [!IMPORTANT]
> Этот класс и его члены не могут использоваться в приложениях, выполняемых в среда выполнения Windows.

## <a name="syntax"></a>Синтаксис

```
template <class T,
    int nBindFlags = BINDF_ASYNCHRONOUS | BINDF_ASYNCSTORAGE | BINDF_GETNEWESTVERSION | BINDF_NOWRITECACHE>
class ATL_NO_VTABLE CBindStatusCallback : public CComObjectRootEx <T ::_ThreadModel::ThreadModelNoCS>,
    public IBindStatusCallbackImpl<T>
```

#### <a name="parameters"></a>Параметры

*T*<br/>
Класс, содержащий функцию, которая будет вызываться при получении данных.

*нбиндфлагс*<br/>
Задает флаги привязки, возвращаемые функцией [GetBindInfo](#getbindinfo). Реализация по умолчанию устанавливает привязку как асинхронную, извлекает последнюю версию данных или объекта и не сохраняет извлеченные данные в кэш диска.

## <a name="members"></a>Элементы

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[Кбиндстатускаллбакк:: Кбиндстатускаллбакк](#cbindstatuscallback)|Конструктор.|
|[Кбиндстатускаллбакк:: ~ Кбиндстатускаллбакк](#dtor)|Деструктор|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Кбиндстатускаллбакк::D гружать](#download)|Статический метод, который запускает процесс загрузки, создает `CBindStatusCallback` объект и вызывает `StartAsyncDownload` .|
|[Кбиндстатускаллбакк:: GetBindInfo](#getbindinfo)|Вызывается асинхронным моникером для запроса информации о типе создаваемой привязки.|
|[Кбиндстатускаллбакк:: предшествовал](#getpriority)|Вызывается асинхронным моникером для получения приоритета операции привязки. Реализация ATL возвращает `E_NOTIMPL` .|
|[Кбиндстатускаллбакк:: Ондатааваилабле](#ondataavailable)|Вызывается для предоставления данных приложению в том виде, в котором оно станет доступным. Считывает данные, а затем вызывает функцию, переданную в нее, для использования данных.|
|[Кбиндстатускаллбакк:: Онловресаурце](#onlowresource)|Вызывается, когда ресурсы имеют низкий уровень. Реализация ATL возвращает S_OK.|
|[Кбиндстатускаллбакк:: Онобжектаваилабле](#onobjectavailable)|Вызывается асинхронным моникером для передачи указателя на интерфейс объекта в приложение. Реализация ATL возвращает S_OK.|
|[Кбиндстатускаллбакк:: OnProgress](#onprogress)|Вызывается для указания хода процесса загрузки данных. Реализация ATL возвращает S_OK.|
|[Кбиндстатускаллбакк:: Онстартбиндинг](#onstartbinding)|Вызывается при запуске привязки.|
|[Кбиндстатускаллбакк:: Онстопбиндинг](#onstopbinding)|Вызывается при остановке асинхронной пересылки данных.|
|[Кбиндстатускаллбакк:: Стартасинкдовнлоад](#startasyncdownload)|Инициализирует доступные байты и байты, считанные в ноль, создает объект потока Push-Type из URL-адреса и вызывает `OnDataAvailable` каждый раз, когда доступны все данные.|

### <a name="public-data-members"></a>Открытые члены данных

|Имя|Описание|
|----------|-----------------|
|[Кбиндстатускаллбакк:: m_dwAvailableToRead](#m_dwavailabletoread)|Число байтов, доступных для чтения.|
|[Кбиндстатускаллбакк:: m_dwTotalRead](#m_dwtotalread)|Общее число считанных байтов.|
|[Кбиндстатускаллбакк:: m_pFunc](#m_pfunc)|Указатель на функцию, вызываемую, когда данные доступны.|
|[Кбиндстатускаллбакк:: m_pT](#m_pt)|Указатель на объект, запрашивающий асинхронную пересылку данных.|
|[Кбиндстатускаллбакк:: m_spBindCtx](#m_spbindctx)|Указатель на интерфейс [IBindCtx](/windows/win32/api/objidl/nn-objidl-ibindctx) для текущей операции привязки.|
|[Кбиндстатускаллбакк:: m_spBinding](#m_spbinding)|Указатель на `IBinding` интерфейс для текущей операции привязки.|
|[Кбиндстатускаллбакк:: m_spMoniker](#m_spmoniker)|Указатель на интерфейс [IMoniker](/windows/win32/api/objidl/nn-objidl-imoniker) для используемого URL-адреса.|
|[Кбиндстатускаллбакк:: m_spStream](#m_spstream)|Указатель на интерфейс [IStream](/windows/win32/api/objidl/nn-objidl-istream) для перемещения данных.|

## <a name="remarks"></a>Комментарии

Класс `CBindStatusCallback` реализует интерфейс `IBindStatusCallback`. `IBindStatusCallback` должен быть реализован приложением, чтобы он мог получать уведомления от асинхронной пересылки данных. В асинхронном моникере, предоставляемом системой, используются `IBindStatusCallback` методы для отправки и получения сведений об асинхронной передаче данных в объект и из него.

Как правило, `CBindStatusCallback` объект связан с определенной операцией привязки. Например, в примере [Async](../../overview/visual-cpp-samples.md) при задании свойства URL-адреса создается `CBindStatusCallback` объект в вызове `Download` :

[!code-cpp[NVC_ATL_Windowing#86](../../atl/codesnippet/cpp/cbindstatuscallback-class_1.h)]

Асинхронное моникер использует функцию обратного вызова `OnData` для вызова приложения, когда оно содержит данные. Асинхронное моникер предоставляется системой.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`CComObjectRootBase`

`IBindStatusCallback`

[CComObjectRootEx](../../atl/reference/ccomobjectrootex-class.md)

`CBindStatusCallback`

## <a name="requirements"></a>Требования

**Заголовок:** атлктл. h

## <a name="cbindstatuscallbackcbindstatuscallback"></a><a name="cbindstatuscallback"></a> Кбиндстатускаллбакк:: Кбиндстатускаллбакк

Конструктор.

```
CBindStatusCallback();
```

### <a name="remarks"></a>Комментарии

Создает объект для получения уведомлений, касающихся асинхронной пересылки данных. Как правило, для каждой операции привязки создается один объект.

Конструктор также инициализирует [m_pT](#m_pt) и [m_pFunc](#m_pfunc) в NULL.

## <a name="cbindstatuscallbackcbindstatuscallback"></a><a name="dtor"></a> Кбиндстатускаллбакк:: ~ Кбиндстатускаллбакк

Деструктор

```
~CBindStatusCallback();
```

### <a name="remarks"></a>Комментарии

Освобождает все выделенные ресурсы.

## <a name="cbindstatuscallbackdownload"></a><a name="download"></a> Кбиндстатускаллбакк::D гружать

Создает `CBindStatusCallback` объект и вызывает метод `StartAsyncDownload` , чтобы начать асинхронную загрузку данных с указанного URL-адреса.

```
static HRESULT Download(
    T* pT,
    ATL_PDATAAVAILABLE pFunc,
    BSTR bstrURL,
    IUnknown* pUnkContainer = NULL,
    BOOL bRelative = FALSE);
```

### <a name="parameters"></a>Параметры

*Лутор*<br/>
окне Указатель на объект, запрашивающий асинхронную пересылку данных. `CBindStatusCallback`Объект преобразованный в классе этого объекта.

*pFunc*<br/>
окне Указатель на функцию, которая получает считанные данные. Функция является членом класса объекта типа `T` . Синтаксис и пример см. в разделе [стартасинкдовнлоад](#startasyncdownload) .

*бструрл*<br/>
окне URL-адрес для получения данных. Может быть любым допустимым URL-адресом или именем файла. Не может быть NULL. Пример:

`CComBSTR mybstr =_T("http://somesite/data.htm")`

*пункконтаинер*<br/>
окне Объект `IUnknown` контейнера. По умолчанию имеет значение NULL.

*брелативе*<br/>
окне Флаг, указывающий, является ли URL-адрес относительным или абсолютным. Значение FALSE по умолчанию, означающее, что URL-адрес является абсолютным.

### <a name="return-value"></a>Возвращаемое значение

Одно из стандартных значений HRESULT.

### <a name="remarks"></a>Комментарии

Каждый раз, когда все данные доступны, они отправляются в объект через `OnDataAvailable` . `OnDataAvailable` считывает данные и вызывает функцию, на которую указывает *pFunc* (например, для сохранения данных или вывода их на экран).

## <a name="cbindstatuscallbackgetbindinfo"></a><a name="getbindinfo"></a> Кбиндстатускаллбакк:: GetBindInfo

Вызывается, чтобы сообщить моникеру, как выполнить привязку.

```
STDMETHOD(GetBindInfo)(
    DWORD* pgrfBSCF,
    BINDINFO* pbindinfo);
```

### <a name="parameters"></a>Параметры

*пгрфбскф*<br/>
заполняет Указатель на значения перечисления БИНДФ, указывающий, как должна выполняться операция привязки. По умолчанию задается со следующими значениями перечисления:

BINDF_ASYNCHRONOUS асинхронную загрузку.

BINDF_ASYNCSTORAGE `OnDataAvailable` возвращает E_PENDING, когда данные еще недоступны, а не блокируются до тех пор, пока данные не будут доступны.

BINDF_GETNEWESTVERSION операция привязки должна получить последнюю версию данных.

BINDF_NOWRITECACHE операция привязки не должна хранить извлеченные данные в кэш диска.

*пбиндинфо*<br/>
[вход, выход] Указатель на `BINDINFO` структуру предоставляет дополнительные сведения о том, как происходит привязка объекта.

### <a name="return-value"></a>Возвращаемое значение

Одно из стандартных значений HRESULT.

### <a name="remarks"></a>Комментарии

Реализация по умолчанию устанавливает привязку как асинхронную и использует модель принудительной передачи данных. В модели передачи данных моникер управляет асинхронной операцией привязки и постоянно уведомляет клиента каждый раз, когда новые данные доступны.

## <a name="cbindstatuscallbackgetpriority"></a><a name="getpriority"></a> Кбиндстатускаллбакк:: предшествовал

Вызывается асинхронным моникером для получения приоритета операции привязки.

```
STDMETHOD(GetPriority)(LONG* pnPriority);
```

### <a name="parameters"></a>Параметры

*пнприорити*<br/>
заполняет Адрес переменной **Long** , которая в случае успеха получает приоритет.

### <a name="return-value"></a>Возвращаемое значение

Возвращает E_NOTIMPL.

## <a name="cbindstatuscallbackm_dwavailabletoread"></a><a name="m_dwavailabletoread"></a> Кбиндстатускаллбакк:: m_dwAvailableToRead

Может использоваться для хранения числа доступных для чтения байтов.

```
DWORD m_dwAvailableToRead;
```

### <a name="remarks"></a>Комментарии

Инициализировано до нуля в `StartAsyncDownload` .

## <a name="cbindstatuscallbackm_dwtotalread"></a><a name="m_dwtotalread"></a> Кбиндстатускаллбакк:: m_dwTotalRead

Совокупное число байтов, считанных при асинхронной передаваемой данных.

```
DWORD m_dwTotalRead;
```

### <a name="remarks"></a>Комментарии

Каждый раз увеличивается на единицу `OnDataAvailable` , чем число фактически считанных байтов. Инициализировано до нуля в `StartAsyncDownload` .

## <a name="cbindstatuscallbackm_pfunc"></a><a name="m_pfunc"></a> Кбиндстатускаллбакк:: m_pFunc

Функция, на которую указывает by, `m_pFunc` вызывается `OnDataAvailable` после считывания доступных данных (например, для сохранения данных или вывода их на экран).

```
ATL_PDATAAVAILABLE m_pFunc;
```

### <a name="remarks"></a>Комментарии

Функция, на которую указывает, `m_pFunc` является членом класса объекта и имеет следующий синтаксис:

```cpp
void Function_Name(
   CBindStatusCallback<T>* pbsc,
   BYTE* pBytes,
   DWORD dwSize
   );
```

## <a name="cbindstatuscallbackm_pt"></a><a name="m_pt"></a> Кбиндстатускаллбакк:: m_pT

Указатель на объект, запрашивающий асинхронную пересылку данных.

```
T* m_pT;
```

### <a name="remarks"></a>Комментарии

`CBindStatusCallback`Объект преобразованный в классе этого объекта.

## <a name="cbindstatuscallbackm_spbindctx"></a><a name="m_spbindctx"></a> Кбиндстатускаллбакк:: m_spBindCtx

Указатель на интерфейс [IBindCtx](/windows/win32/api/objidl/nn-objidl-ibindctx) , предоставляющий доступ к контексту привязки (объект, хранящий сведения о конкретной операции привязки моникера).

```
CComPtr<IBindCtx> m_spBindCtx;
```

### <a name="remarks"></a>Комментарии

Инициализирован в `StartAsyncDownload` .

## <a name="cbindstatuscallbackm_spbinding"></a><a name="m_spbinding"></a> Кбиндстатускаллбакк:: m_spBinding

Указатель на `IBinding` интерфейс текущей операции привязки.

```
CComPtr<IBinding> m_spBinding;
```

### <a name="remarks"></a>Комментарии

Инициализируется в `OnStartBinding` и выпускается в `OnStopBinding` .

## <a name="cbindstatuscallbackm_spmoniker"></a><a name="m_spmoniker"></a> Кбиндстатускаллбакк:: m_spMoniker

Указатель на интерфейс [IMoniker](/windows/win32/api/objidl/nn-objidl-imoniker) для используемого URL-адреса.

```
CComPtr<IMoniker> m_spMoniker;
```

### <a name="remarks"></a>Комментарии

Инициализирован в `StartAsyncDownload` .

## <a name="cbindstatuscallbackm_spstream"></a><a name="m_spstream"></a> Кбиндстатускаллбакк:: m_spStream

Указатель на интерфейс [IStream](/windows/win32/api/objidl/nn-objidl-istream) текущей операции привязки.

```
CComPtr<IStream> m_spStream;
```

### <a name="remarks"></a>Комментарии

Инициализируется в `OnDataAvailable` из `STGMEDIUM` структуры, когда флаг бксф BCSF_FIRSTDATANOTIFICATION и освобождается при BCSF_LASTDATANOTIFICATION флаге бксф.

## <a name="cbindstatuscallbackondataavailable"></a><a name="ondataavailable"></a> Кбиндстатускаллбакк:: Ондатааваилабле

Предоставляемые системой асинхронные вызовы моникера `OnDataAvailable` для предоставления данных объекту в том виде, в котором они становятся доступными.

```
STDMETHOD(
    OnDataAvailable)(DWORD grfBSCF,
    DWORD dwSize,
    FORMATETC* /* pformatetc */,
    STGMEDIUM* pstgmed);
```

### <a name="parameters"></a>Параметры

*грфбскф*<br/>
окне Значение перечисления БСКФ. Один или несколько из следующих элементов: BSCF_FIRSTDATANOTIFICATION, BSCF_INTERMEDIARYDATANOTIFICATION или BSCF_LASTDATANOTIFICATION.

*двсизе*<br/>
окне Совокупный объем данных (в байтах), доступный с начала привязки. Может быть равно нулю, что означает, что объем данных не важен или не стал доступным никакой конкретной суммы.

*пформатетк*<br/>
окне Указатель на структуру [форматетк](/windows/win32/com/the-formatetc-structure) , которая содержит формат доступных данных. Если формат отсутствует, можно CF_NULL.

*пстгмед*<br/>
окне Указатель на структуру [стгмедиум](/windows/win32/com/the-stgmedium-structure) , содержащую фактические данные, которые теперь доступны.

### <a name="return-value"></a>Возвращаемое значение

Одно из стандартных значений HRESULT.

### <a name="remarks"></a>Комментарии

`OnDataAvailable` считывает данные, а затем вызывает метод класса объекта (например, для сохранения данных или вывода их на экран). Дополнительные сведения см. в разделе [кбиндстатускаллбакк:: стартасинкдовнлоад](#startasyncdownload) .

## <a name="cbindstatuscallbackonlowresource"></a><a name="onlowresource"></a> Кбиндстатускаллбакк:: Онловресаурце

Вызывается, когда ресурсы имеют низкий уровень.

```
STDMETHOD(OnLowResource)(DWORD /* dwReserved */);
```

### <a name="parameters"></a>Параметры

*двресервед*<br/>
Зарезервировано.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK.

## <a name="cbindstatuscallbackonobjectavailable"></a><a name="onobjectavailable"></a> Кбиндстатускаллбакк:: Онобжектаваилабле

Вызывается асинхронным моникером для передачи указателя на интерфейс объекта в приложение.

```
STDMETHOD(OnObjectAvailable)(REFID /* riid */, IUnknown* /* punk */);
```

### <a name="parameters"></a>Параметры

*riid*<br/>
Идентификатор интерфейса запрошенного интерфейса. Не используется.

*Punk*<br/>
Адрес интерфейса IUnknown. Не используется.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK.

## <a name="cbindstatuscallbackonprogress"></a><a name="onprogress"></a> Кбиндстатускаллбакк:: OnProgress

Вызывается для указания хода процесса загрузки данных.

```
STDMETHOD(OnProgress)(
    ULONG /* ulProgress */,
    ULONG /* ulProgressMax */,
    ULONG /* ulStatusCode */,
    LPCWSTRONG /* szStatusText */);
```

### <a name="parameters"></a>Параметры

*улпрогресс*<br/>
Длинное целое число без знака. Не используется.

*улпрогрессмакс*<br/>
Неиспользуемое длинное целое без знака.

*улстатускоде*<br/>
Длинное целое число без знака. Не используется.

*сзстатустекст*<br/>
Адрес строкового значения. Не используется.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK.

## <a name="cbindstatuscallbackonstartbinding"></a><a name="onstartbinding"></a> Кбиндстатускаллбакк:: Онстартбиндинг

Задает [m_spBinding](#m_spbinding) элемента данных `IBinding` указатель в *пбиндинг*.

```
STDMETHOD(OnStartBinding)(DWORD /* dwReserved */, IBinding* pBinding);
```

### <a name="parameters"></a>Параметры

*двресервед*<br/>
Зарезервировано для будущего использования.

*пбиндинг*<br/>
окне Адрес интерфейса Ибиндинг текущей операции привязки. Это значение не может быть равно NULL. Клиент должен вызвать AddRef для этого указателя, чтобы удержать ссылку на объект привязки.

## <a name="cbindstatuscallbackonstopbinding"></a><a name="onstopbinding"></a> Кбиндстатускаллбакк:: Онстопбиндинг

Освобождает `IBinding` указатель в элементе данных [m_spBinding](#m_spbinding).

```
STDMETHOD(OnStopBinding)(HRESULT hresult, LPCWSTR /* szError */);
```

### <a name="parameters"></a>Параметры

*состав*<br/>
Код состояния, возвращенный операцией привязки.

*сзеррор*<br/>
Адрес строкового значения. Не используется.

### <a name="remarks"></a>Комментарии

Вызывается предоставляемым системой асинхронным моникером для обозначения конца операции привязки.

## <a name="cbindstatuscallbackstartasyncdownload"></a><a name="startasyncdownload"></a> Кбиндстатускаллбакк:: Стартасинкдовнлоад

Запускает асинхронную загрузку данных по указанному URL-адресу.

```
HRESULT StartAsyncDownload(
    T* pT,
    ATL_PDATAAVAILABLE pFunc,
    BSTR bstrURL,
    IUnknown* pUnkContainer = NULL,
    BOOL bRelative = FALSE);
```

### <a name="parameters"></a>Параметры

*Лутор*<br/>
окне Указатель на объект, запрашивающий асинхронную пересылку данных. `CBindStatusCallback`Объект преобразованный в классе этого объекта.

*pFunc*<br/>
окне Указатель на функцию, которая получает считываемые данные. Функция является членом класса объекта типа `T` . Синтаксис и пример см. в разделе **Примечания** .

*бструрл*<br/>
окне URL-адрес для получения данных. Может быть любым допустимым URL-адресом или именем файла. Не может быть NULL. Пример:

`CComBSTR mybstr =_T("http://somesite/data.htm")`

*пункконтаинер*<br/>
окне Объект `IUnknown` контейнера. По умолчанию имеет значение NULL.

*брелативе*<br/>
окне Флаг, указывающий, является ли URL-адрес относительным или абсолютным. Значение FALSE по умолчанию, означающее, что URL-адрес является абсолютным.

### <a name="return-value"></a>Возвращаемое значение

Одно из стандартных значений HRESULT.

### <a name="remarks"></a>Комментарии

Каждый раз, когда все данные доступны, они отправляются в объект через `OnDataAvailable` . `OnDataAvailable` считывает данные и вызывает функцию, на которую указывает *pFunc* (например, для сохранения данных или вывода их на экран).

Функция, на которую указывает *pFunc* , является членом класса объекта и имеет следующий синтаксис:

```cpp
void Function_Name(
    CBindStatusCallback<T>* pbsc,
    BYTE* pBytes,
    DWORD dwSize);
```

В следующем примере (взятом из примера [Async](../../overview/visual-cpp-samples.md) ) функция `OnData` записывает полученные данные в текстовое поле.

### <a name="example"></a>Пример

[!code-cpp[NVC_ATL_Windowing#87](../../atl/codesnippet/cpp/cbindstatuscallback-class_2.h)]

## <a name="see-also"></a>См. также раздел

[Общие сведения о классах](../../atl/atl-class-overview.md)
