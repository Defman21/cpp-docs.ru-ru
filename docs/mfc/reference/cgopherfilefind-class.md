---
description: 'Дополнительные сведения о: Кгоферфилефинд Class'
title: Класс Кгоферфилефинд
ms.date: 11/04/2016
f1_keywords:
- CGopherFileFind
- AFXINET/CGopherFileFind
- AFXINET/CGopherFileFind::CGopherFileFind
- AFXINET/CGopherFileFind::FindFile
- AFXINET/CGopherFileFind::FindNextFile
- AFXINET/CGopherFileFind::GetCreationTime
- AFXINET/CGopherFileFind::GetLastAccessTime
- AFXINET/CGopherFileFind::GetLastWriteTime
- AFXINET/CGopherFileFind::GetLength
- AFXINET/CGopherFileFind::GetLocator
- AFXINET/CGopherFileFind::GetScreenName
- AFXINET/CGopherFileFind::IsDots
helpviewer_keywords:
- CGopherFileFind [MFC], CGopherFileFind
- CGopherFileFind [MFC], FindFile
- CGopherFileFind [MFC], FindNextFile
- CGopherFileFind [MFC], GetCreationTime
- CGopherFileFind [MFC], GetLastAccessTime
- CGopherFileFind [MFC], GetLastWriteTime
- CGopherFileFind [MFC], GetLength
- CGopherFileFind [MFC], GetLocator
- CGopherFileFind [MFC], GetScreenName
- CGopherFileFind [MFC], IsDots
ms.assetid: 8465a979-6323-496d-ab4b-e81383fb999d
ms.openlocfilehash: 483a0a6221d08cc3821b0dbc44dd1003c0c40114
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97184053"
---
# <a name="cgopherfilefind-class"></a>Класс Кгоферфилефинд

Помогает в поиске файлов Интернета на серверах gopher.

> [!NOTE]
> Классы `CGopherConnection` ,, `CGopherFile` `CGopherFileFind` `CGopherLocator` и их члены являются устаревшими, так как они не работают на платформе Windows XP, но они продолжат работать на более ранних платформах.

## <a name="syntax"></a>Синтаксис

```
class CGopherFileFind : public CFileFind
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|name|Описание|
|----------|-----------------|
|[Кгоферфилефинд:: Кгоферфилефинд](#cgopherfilefind)|Формирует объект `CGopherFileFind`.|

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[Кгоферфилефинд:: Финдфиле](#findfile)|Находит файл на сервере Gopher.|
|[Кгоферфилефинд:: FindNextFile](#findnextfile)|Возобновляет Поиск файла из предыдущего вызова [финдфиле](#findfile).|
|[Кгоферфилефинд:: Жеткреатионтиме](#getcreationtime)|Возвращает время создания указанного файла.|
|[Кгоферфилефинд:: Жетластакцесстиме](#getlastaccesstime)|Возвращает время последнего обращения к указанному файлу.|
|[Кгоферфилефинд:: Жетластвритетиме](#getlastwritetime)|Возвращает время последней запись в указанный файл.|
|[Кгоферфилефинд:: DATALENGTH](#getlength)|Возвращает длину найденного файла в байтах.|
|[Кгоферфилефинд:: Locator](#getlocator)|Получение `CGopherLocator` объекта.|
|[Кгоферфилефинд:: Жетскриннаме](#getscreenname)|Возвращает имя Gopher-экрана.|
|[Кгоферфилефинд:: наТочки](#isdots)|Проверяет наличие маркеров текущего каталога и родительского каталога при переборе файлов.|

## <a name="remarks"></a>Комментарии

`CGopherFileFind` содержит функции-члены, которые начинают поиск, находят файл и возвращает URL-адрес файла.

Другие классы MFC, предназначенные для поиска в Интернете и локальном файле, включают [кфтпфилефинд](../../mfc/reference/cftpfilefind-class.md) и [кфилефинд](../../mfc/reference/cfilefind-class.md). Вместе с `CGopherFileFind` эти классы предоставляют пользователю простой механизм поиска конкретных файлов независимо от протокола сервера, типа файла или расположения (локального или удаленного сервера). Обратите внимание, что отсутствует класс MFC для поиска на HTTP-серверах, так как HTTP не поддерживает прямую обработку файлов, необходимую для поиска.

> [!NOTE]
> `CGopherFileFind` не поддерживает следующие функции элементов базового класса [кфилефинд](../../mfc/reference/cfilefind-class.md):

- [GetRoot](../../mfc/reference/cfilefind-class.md#getroot)

- [GetFileName](../../mfc/reference/cfilefind-class.md#getfilename)

- [Путь к файлу](../../mfc/reference/cfilefind-class.md#getfilepath)

- [жетфилетитле](../../mfc/reference/cfilefind-class.md#getfiletitle)

- [жетфилеурл](../../mfc/reference/cfilefind-class.md#getfileurl)

Кроме того, при использовании с `CGopherFileFind` `CFileFind` функция-член всегда [](../../mfc/reference/cfilefind-class.md#isdots) имеет значение false.

Дополнительные сведения об использовании `CGopherFileFind` и других классах WinInet см. в статье [Интернет – программирование с помощью WinInet](../../mfc/win32-internet-extensions-wininet.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[CObject](../../mfc/reference/cobject-class.md)

[CFileFind](../../mfc/reference/cfilefind-class.md)

`CGopherFileFind`

## <a name="requirements"></a>Требования

**Заголовок:** афксинет. h

## <a name="cgopherfilefindcgopherfilefind"></a><a name="cgopherfilefind"></a> Кгоферфилефинд:: Кгоферфилефинд

Эта функция-член вызывается для создания `CGopherFileFind` объекта.

```
explicit CGopherFileFind(
    CGopherConnection* pConnection,
    DWORD_PTR dwContext = 1);
```

### <a name="parameters"></a>Параметры

*пконнектион*<br/>
Указатель на объект [кгоферконнектион](../../mfc/reference/cgopherconnection-class.md) .

*двконтекст*<br/>
Идентификатор контекста для операции. Дополнительные сведения о *двконтекст* см. в разделе **Примечания** .

### <a name="remarks"></a>Комментарии

Значение по умолчанию для *двконтекст* отправляется MFC `CGopherFileFind` объекту из объекта [Цинтернетсессион](../../mfc/reference/cinternetsession-class.md) , который создал `CGopherFileFind` объект. При создании `CGopherFileFind` объекта можно переопределить значение по умолчанию, чтобы задать идентификатор контекста в качестве значения по своему усмотрению. Идентификатор контекста возвращается в [Цинтернетсессион:: онстатускаллбакк](../../mfc/reference/cinternetsession-class.md#onstatuscallback) , чтобы предоставить состояние для объекта, с которым он определен. Дополнительные сведения об идентификаторе контекста см. в статье [первые шаги в Интернете: WinInet](../../mfc/wininet-basics.md) .

## <a name="cgopherfilefindfindfile"></a><a name="findfile"></a> Кгоферфилефинд:: Финдфиле

Вызовите эту функцию-член для поиска файла gopher.

```
virtual BOOL FindFile(
    CGopherLocator& refLocator,
    LPCTSTR pstrString,
    DWORD dwFlags = INTERNET_FLAG_RELOAD);

virtual BOOL FindFile(
    LPCTSTR pstrString,
    DWORD dwFlags = INTERNET_FLAG_RELOAD);
```

### <a name="parameters"></a>Параметры

*рефлокатор*<br/>
Ссылка на объект [кгоферлокатор](../../mfc/reference/cgopherlocator-class.md) .

*пстрстринг*<br/>
Указатель на строку, содержащую имя файла.

*dwFlags*<br/>
Флаги, описывающие способ управления этим сеансом. Допустимые флаги:

- INTERNET_FLAG_RELOAD получить данные с удаленного сервера, даже если они кэшируются локально.

- INTERNET_FLAG_DONT_CACHE не кэшировать данные локально или в любых шлюзах.

- INTERNET_FLAG_SECURE запрашивать защищенные транзакции в сети с помощью SSL или PCT. Этот флаг применим только к HTTP-запросам.

- INTERNET_FLAG_USE_EXISTING по возможности повторно используйте существующие подключения к серверу для новых `FindFile` запросов вместо создания нового сеанса для каждого запроса.

### <a name="return-value"></a>Возвращаемое значение

Имеет ненулевое значение в случае успешного выполнения, иначе — 0. Чтобы получить расширенные сведения об ошибке, вызовите функцию Win32 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror).

### <a name="remarks"></a>Комментарии

После вызова `FindFile` для получения первого объекта Gopher можно вызвать [FindNextFile](#findnextfile) для получения последующих файлов Gopher.

## <a name="cgopherfilefindfindnextfile"></a><a name="findnextfile"></a> Кгоферфилефинд:: FindNextFile

Вызовите эту функцию-член, чтобы продолжить поиск файла, начатый вызовом [кгоферфилефинд:: финдфиле](#findfile).

```
virtual BOOL FindNextFile();
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если есть больше файлов; нуль, если найденный файл является последним в каталоге или если произошла ошибка. Чтобы получить расширенные сведения об ошибке, вызовите функцию Win32 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror). Если найденный файл является последним файлом в каталоге или не удается найти соответствующие файлы, `GetLastError` функция возвращает ERROR_NO_MORE_FILES.

## <a name="cgopherfilefindgetcreationtime"></a><a name="getcreationtime"></a> Кгоферфилефинд:: Жеткреатионтиме

Возвращает время создания текущего файла.

```
virtual BOOL GetCreationTime(FILETIME* pTimeStamp) const;
virtual BOOL GetCreationTime(CTime& refTime) const;
```

### <a name="parameters"></a>Параметры

*птиместамп*<br/>
Указатель на структуру [fileTime](/windows/win32/api/minwinbase/ns-minwinbase-filetime) , содержащую время создания файла.

*рефтиме*<br/>
Ссылка на объект [CTime](../../atl-mfc-shared/reference/ctime-class.md) .

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение в случае успешного выполнения; 0 в случае неудачи. `GetCreationTime` Возвращает 0, только если для этого объекта никогда не вызывался [FindNextFile](#findnextfile) `CGopherFileFind` .

### <a name="remarks"></a>Комментарии

Необходимо вызвать [FindNextFile](#findnextfile) по крайней мере один раз перед вызовом `GetCreationTime` .

> [!NOTE]
> Не все файловые системы используют одну и ту же семантику для реализации отметки времени, возвращаемой этой функцией. Эта функция может возвращать то же значение, что и другие функции отметки времени, если базовая файловая система или сервер не поддерживает поддержание атрибута времени. Сведения о форматах времени см. в разделе Структура [WIN32_FIND_DATA](/windows/win32/api/minwinbase/ns-minwinbase-win32_find_dataw) . В некоторых операционных системах возвращенное время находится на локальном часовом поясе компьютера, где находится файл. Дополнительные сведения см. в разделе API Win32 [филетиметолокалфилетиме](/windows/win32/api/fileapi/nf-fileapi-filetimetolocalfiletime) .

## <a name="cgopherfilefindgetlastaccesstime"></a><a name="getlastaccesstime"></a> Кгоферфилефинд:: Жетластакцесстиме

Возвращает время последнего обращения к указанному файлу.

```
virtual BOOL GetLastAccessTime(CTime& refTime) const;
virtual BOOL GetLastAccessTime(FILETIME* pTimeStamp) const;
```

### <a name="parameters"></a>Параметры

*рефтиме*<br/>
Ссылка на объект [CTime](../../atl-mfc-shared/reference/ctime-class.md) .

*птиместамп*<br/>
Указатель на структуру [fileTime](/windows/win32/api/minwinbase/ns-minwinbase-filetime) , содержащую время последнего обращения к файлу.

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение в случае успешного выполнения; 0 в случае неудачи. `GetLastAccessTime` Возвращает 0, только если для этого объекта никогда не вызывался [FindNextFile](#findnextfile) `CGopherFileFind` .

### <a name="remarks"></a>Комментарии

Необходимо вызвать [FindNextFile](#findnextfile) по крайней мере один раз перед вызовом `GetLastAccessTime` .

> [!NOTE]
> Не все файловые системы используют одну и ту же семантику для реализации отметки времени, возвращаемой этой функцией. Эта функция может возвращать то же значение, что и другие функции отметки времени, если базовая файловая система или сервер не поддерживает поддержание атрибута времени. Сведения о форматах времени см. в разделе Структура [WIN32_FIND_DATA](/windows/win32/api/minwinbase/ns-minwinbase-win32_find_dataw) . В некоторых операционных системах возвращенное время находится на локальном часовом поясе компьютера, где находится файл. Дополнительные сведения см. в разделе API Win32 [филетиметолокалфилетиме](/windows/win32/api/fileapi/nf-fileapi-filetimetolocalfiletime) .

## <a name="cgopherfilefindgetlastwritetime"></a><a name="getlastwritetime"></a> Кгоферфилефинд:: Жетластвритетиме

Возвращает время последнего изменения файла.

```
virtual BOOL GetLastWriteTime(FILETIME* pTimeStamp) const;
virtual BOOL GetLastWriteTime(CTime& refTime) const;
```

### <a name="parameters"></a>Параметры

*птиместамп*<br/>
Указатель на структуру [fileTime](/windows/win32/api/minwinbase/ns-minwinbase-filetime) , содержащую время последней запись в файл.

*рефтиме*<br/>
Ссылка на объект [CTime](../../atl-mfc-shared/reference/ctime-class.md) .

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение в случае успешного выполнения; 0 в случае неудачи. `GetLastWriteTime` Возвращает 0, только если для этого объекта никогда не вызывался [FindNextFile](#findnextfile) `CGopherFileFind` .

### <a name="remarks"></a>Комментарии

Необходимо вызвать [FindNextFile](#findnextfile) по крайней мере один раз перед вызовом `GetLastWriteTime` .

> [!NOTE]
> Не все файловые системы используют одну и ту же семантику для реализации отметки времени, возвращаемой этой функцией. Эта функция может возвращать то же значение, что и другие функции отметки времени, если базовая файловая система или сервер не поддерживает поддержание атрибута времени. Сведения о форматах времени см. в разделе Структура [WIN32_FIND_DATA](/windows/win32/api/minwinbase/ns-minwinbase-win32_find_dataw) . В некоторых операционных системах возвращенное время находится на локальном часовом поясе компьютера, где находится файл. Дополнительные сведения см. в разделе API Win32 [филетиметолокалфилетиме](/windows/win32/api/fileapi/nf-fileapi-filetimetolocalfiletime) .

## <a name="cgopherfilefindgetlength"></a><a name="getlength"></a> Кгоферфилефинд:: DATALENGTH

Вызовите эту функцию члена, чтобы получить длину найденного файла в байтах.

```
virtual ULONGLONG GetLength() const;
```

### <a name="return-value"></a>Возвращаемое значение

Длина найденного файла в байтах.

### <a name="remarks"></a>Комментарии

`GetLength` использует структуру Win32 [WIN32_FIND_DATA](/windows/win32/api/minwinbase/ns-minwinbase-win32_find_dataw) для получения значения размера файла в байтах.

> [!NOTE]
> Начиная с MFC 7,0 `GetLength` поддерживает 64-разрядные целочисленные типы. Ранее существующий код, созданный с помощью этой более новой версии библиотеки, может привести к предупреждениям усечения.

### <a name="example"></a>Пример

  См. пример для [кфиле:: DATALENGTH](../../mfc/reference/cfile-class.md#getlength) (реализация базового класса).

## <a name="cgopherfilefindgetlocator"></a><a name="getlocator"></a> Кгоферфилефинд:: Locator

Вызовите эту функцию члена, чтобы получить объект [кгоферлокатор](../../mfc/reference/cgopherlocator-class.md) , который [финдфиле](#findfile) использует для поиска файла gopher.

```
CGopherLocator GetLocator() const;
```

### <a name="return-value"></a>Возвращаемое значение

Объект `CGopherLocator`.

## <a name="cgopherfilefindgetscreenname"></a><a name="getscreenname"></a> Кгоферфилефинд:: Жетскриннаме

Вызовите эту функцию члена для получения имени экрана Gopher.

```
CString GetScreenName() const;
```

### <a name="return-value"></a>Возвращаемое значение

Имя экрана Gopher.

## <a name="cgopherfilefindisdots"></a><a name="isdots"></a> Кгоферфилефинд:: наТочки

Проверяет наличие маркеров текущего каталога и родительского каталога при переборе файлов.

```
virtual BOOL IsDots() const;
```

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если найденный файл имеет имя "." или "..", что означает, что найденный файл действительно является каталогом. В противном случае 0.

### <a name="remarks"></a>Комментарии

Необходимо вызвать [FindNextFile](#findnextfile) по крайней мере один раз перед вызовом `IsDots` .

## <a name="see-also"></a>См. также раздел

[Класс Кфилефинд](../../mfc/reference/cfilefind-class.md)<br/>
[Иерархическая диаграмма](../../mfc/hierarchy-chart.md)<br/>
[Класс Кфтпфилефинд](../../mfc/reference/cftpfilefind-class.md)<br/>
[Класс Кфилефинд](../../mfc/reference/cfilefind-class.md)<br/>
[Класс Цинтернетфиле](../../mfc/reference/cinternetfile-class.md)<br/>
[Класс CGopherFile](../../mfc/reference/cgopherfile-class.md)<br/>
[Класс Чттпфиле](../../mfc/reference/chttpfile-class.md)
