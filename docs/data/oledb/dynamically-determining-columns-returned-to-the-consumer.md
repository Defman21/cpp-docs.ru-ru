---
description: 'Дополнительные сведения: динамическое определение столбцов, возвращаемых потребителю'
title: Динамично определяемые столбцы, возвращенные объекту-получателю
ms.date: 10/26/2018
helpviewer_keywords:
- bookmarks [C++], dynamically determining columns
- dynamically determining columns [C++]
ms.assetid: 58522b7a-894e-4b7d-a605-f80e900a7f5f
ms.openlocfilehash: fd70164edff5b9267e01a891a143920ac4e60a35
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97287571"
---
# <a name="dynamically-determining-columns-returned-to-the-consumer"></a>Динамично определяемые столбцы, возвращенные объекту-получателю

Макросы PROVIDER_COLUMN_ENTRY обычно обрабатывали `IColumnsInfo::GetColumnsInfo` вызов. Однако, поскольку потребитель может выбрать использование закладок, поставщик должен иметь возможность изменять столбцы, возвращаемые в зависимости от того, запрашивает ли потребитель закладку.

Чтобы обрабатывался `IColumnsInfo::GetColumnsInfo` вызов, удалите PROVIDER_COLUMN_MAP, определяющую функцию `GetColumnInfo` , из `CCustomWindowsFile` записи пользователя в *пользовательском* RS. h и замените ее определением для собственной `GetColumnInfo` функции:

```cpp
////////////////////////////////////////////////////////////////////////
// CustomRS.H
class CCustomWindowsFile
{
public:
   DWORD dwBookmark;
   static const int iSize = 256;
   TCHAR szCommand[iSize];
   TCHAR szText[iSize];
   TCHAR szCommand2[iSize];
   TCHAR szText2[iSize];
  
   static ATLCOLUMNINFO* GetColumnInfo(void* pThis, ULONG* pcCols);
   bool operator==(const CCustomWindowsFile& am)
   {
      return (lstrcmpi(szCommand, am.szCommand) == 0);
   }
};
```

Затем реализуйте `GetColumnInfo` функцию в *пользовательском* RS. cpp, как показано в следующем коде.

`GetColumnInfo` сначала проверяет, задано ли свойство OLE DB `DBPROP_BOOKMARKS` . Чтобы получить свойство, `GetColumnInfo` использует указатель ( `pRowset` ) для объекта набора строк. `pThis`Указатель представляет класс, который создал набор строк, который является классом, в котором хранится схема свойств. `GetColumnInfo` приведение `pThis` указателя к `RCustomRowset` указателю.

Чтобы проверить `DBPROP_BOOKMARKS` свойство, `GetColumnInfo` использует `IRowsetInfo` интерфейс, который можно получить путем вызова метода `QueryInterface` в `pRowset` интерфейсе. В качестве альтернативы можно использовать вместо этого метод ATL [CComQIPtr](../../atl/reference/ccomqiptr-class.md) .

```cpp
////////////////////////////////////////////////////////////////////
// CustomRS.cpp
ATLCOLUMNINFO* CCustomWindowsFile::GetColumnInfo(void* pThis, ULONG* pcCols)
{
   static ATLCOLUMNINFO _rgColumns[5];
   ULONG ulCols = 0;
  
   // Check the property flag for bookmarks; if it is set, set the zero
   // ordinal entry in the column map with the bookmark information.
   CCustomRowset* pRowset = (CCustomRowset*) pThis;
   CComQIPtr<IRowsetInfo, &IID_IRowsetInfo> spRowsetProps = pRowset;
  
   CDBPropIDSet set(DBPROPSET_ROWSET);
   set.AddPropertyID(DBPROP_BOOKMARKS);
   DBPROPSET* pPropSet = NULL;
   ULONG ulPropSet = 0;
   HRESULT hr;
  
   if (spRowsetProps)
      hr = spRowsetProps->GetProperties(1, &set, &ulPropSet, &pPropSet);
  
   if (pPropSet)
   {
      CComVariant var = pPropSet->rgProperties[0].vValue;
      CoTaskMemFree(pPropSet->rgProperties);
      CoTaskMemFree(pPropSet);
  
      if (SUCCEEDED(hr) && (var.boolVal == VARIANT_TRUE))
      {
         ADD_COLUMN_ENTRY_EX(ulCols, OLESTR("Bookmark"), 0, sizeof(DWORD),
         DBTYPE_BYTES, 0, 0, GUID_NULL, CCustomWindowsFile, dwBookmark,
         DBCOLUMNFLAGS_ISBOOKMARK)
         ulCols++;
      }
   }
  
   // Next, set the other columns up.
   ADD_COLUMN_ENTRY(ulCols, OLESTR("Command"), 1, 256, DBTYPE_STR, 0xFF, 0xFF,
      GUID_NULL, CCustomWindowsFile, szCommand)
   ulCols++;
   ADD_COLUMN_ENTRY(ulCols, OLESTR("Text"), 2, 256, DBTYPE_STR, 0xFF, 0xFF,
      GUID_NULL, CCustomWindowsFile, szText)
   ulCols++;
  
   ADD_COLUMN_ENTRY(ulCols, OLESTR("Command2"), 3, 256, DBTYPE_STR, 0xFF, 0xFF,
      GUID_NULL, CCustomWindowsFile, szCommand2)
   ulCols++;
   ADD_COLUMN_ENTRY(ulCols, OLESTR("Text2"), 4, 256, DBTYPE_STR, 0xFF, 0xFF,
      GUID_NULL, CCustomWindowsFile, szText2)
   ulCols++;
  
   if (pcCols != NULL)
      *pcCols = ulCols;
  
   return _rgColumns;
}
```

В этом примере для хранения сведений о столбцах используется статический массив. Если потребителю не нужен столбец закладки, одна запись в массиве не используется. Для работы с данными создаются два макроса массива: ADD_COLUMN_ENTRY и ADD_COLUMN_ENTRY_EX. ADD_COLUMN_ENTRY_EX принимает дополнительный параметр *flags*, который необходим при назначении столбца закладки.

```cpp
////////////////////////////////////////////////////////////////////////  
// CustomRS.h  
  
#define ADD_COLUMN_ENTRY(ulCols, name, ordinal, colSize, type, precision, scale, guid, dataClass, member) \  
   _rgColumns[ulCols].pwszName = (LPOLESTR)name; \  
   _rgColumns[ulCols].pTypeInfo = (ITypeInfo*)NULL; \  
   _rgColumns[ulCols].iOrdinal = (ULONG)ordinal; \  
   _rgColumns[ulCols].dwFlags = 0; \  
   _rgColumns[ulCols].ulColumnSize = (ULONG)colSize; \  
   _rgColumns[ulCols].wType = (DBTYPE)type; \  
   _rgColumns[ulCols].bPrecision = (BYTE)precision; \  
   _rgColumns[ulCols].bScale = (BYTE)scale; \  
   _rgColumns[ulCols].cbOffset = offsetof(dataClass, member);  
  
#define ADD_COLUMN_ENTRY_EX(ulCols, name, ordinal, colSize, type, precision, scale, guid, dataClass, member, flags) \  
   _rgColumns[ulCols].pwszName = (LPOLESTR)name; \  
   _rgColumns[ulCols].pTypeInfo = (ITypeInfo*)NULL; \  
   _rgColumns[ulCols].iOrdinal = (ULONG)ordinal; \  
   _rgColumns[ulCols].dwFlags = flags; \  
   _rgColumns[ulCols].ulColumnSize = (ULONG)colSize; \  
   _rgColumns[ulCols].wType = (DBTYPE)type; \  
   _rgColumns[ulCols].bPrecision = (BYTE)precision; \  
   _rgColumns[ulCols].bScale = (BYTE)scale; \  
   _rgColumns[ulCols].cbOffset = offsetof(dataClass, member); \  
   memset(&(_rgColumns[ulCols].columnid), 0, sizeof(DBID)); \  
   _rgColumns[ulCols].columnid.uName.pwszName = (LPOLESTR)name;  
```

В `GetColumnInfo` функции макрос закладки используется следующим образом:

```cpp
ADD_COLUMN_ENTRY_EX(ulCols, OLESTR("Bookmark"), 0, sizeof(DWORD),
   DBTYPE_BYTES, 0, 0, GUID_NULL, CAgentMan, dwBookmark,
   DBCOLUMNFLAGS_ISBOOKMARK)
```

Теперь можно скомпилировать и запустить Улучшенный поставщик. Чтобы протестировать поставщик, измените тестового потребителя, как описано в разделе [Реализация простого потребителя](../../data/oledb/implementing-a-simple-consumer.md). Запустите тестового потребителя с поставщиком и убедитесь, что тестовый потребитель получает соответствующие строки от поставщика.

## <a name="see-also"></a>См. также раздел

[Усовершенствование простого поставщика Read-Only](../../data/oledb/enhancing-the-simple-read-only-provider.md)<br/>
