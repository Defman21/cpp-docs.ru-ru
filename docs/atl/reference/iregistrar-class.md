---
description: 'Дополнительные сведения о: интерфейс IRegistrar'
title: Интерфейс IRegistrar
ms.date: 02/01/2017
f1_keywords:
- IRegistrar
- ATLIFASE/ATL::IRegistrar
- ATLIFASE/ATL::IRegistrar::ResourceRegisterSz
- ATLIFASE/ATL::IRegistrar::ResourceUnregisterSz
- ATLIFASE/ATL::IRegistrar::FileRegister
- ATLIFASE/ATL::IRegistrar::FileUnregister
- ATLIFASE/ATL::IRegistrar::StringRegister
- ATLIFASE/ATL::IRegistrar::StringUnregister
- ATLIFASE/ATL::IRegistrar::ResourceRegister
- ATLIFASE/ATL::IRegistrar::ResourceUnregister
helpviewer_keywords:
- Iregistrar Interface
ms.assetid: e88c04b7-0c93-4ae8-aeb9-ecd78f87421e
ms.openlocfilehash: 9a138468ccbf21594c4e9d88d1ed2387a4c1052a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2020
ms.locfileid: "97139169"
---
# <a name="iregistrar-interface"></a>Интерфейс IRegistrar

Этот интерфейс определен в описана. h и используется внутренне функциями-членами Катлмодуле, такими как [упдатерегистрифромресаурцед](catlmodule-class.md#updateregistryfromresourced).

## <a name="syntax"></a>Синтаксис

```
typedef interface IRegistrar IRegistrar;
```

## <a name="remarks"></a>Remarks

Дополнительные сведения см. в разделе [Использование заменяемых параметров (препроцессор регистратора)](../../atl/using-replaceable-parameters-the-registrar-s-preprocessor.md) .

## <a name="members"></a>Элементы

### <a name="public-methods"></a>Открытые методы

|name|Описание|
|----------|-----------------|
|[IRegistrar:: Ресаурцерегистерсз](#resourceregistersz)|Регистрирует ресурс. |
|[IRegistrar:: Ресаурцеунрегистерсз](#resourceunregistersz)| Отменяет регистрацию ресурса.|
|[IRegistrar:: Филерегистер](#fileregister)|Регистрирует файл.|
|[IRegistrar:: Филеунрегистер](#fileunregister)|Отменяет регистрацию файла.|
|[IRegistrar:: Стрингрегистер](#stringregister)|Регистрирует строку.|
|[IRegistrar:: Стрингунрегистер](#stringunregister)|Отменяет регистрацию строки|
|[IRegistrar:: Ресаурцерегистер](#resourceregister)|Регистрирует ресурс.|
|[IRegistrar:: Ресаурцеунрегистер](#resourceunregister)|Отменяет регистрацию ресурса.|

## <a name="requirements"></a>Требования

**Заголовок:** атлифасе. h

## <a name="iregistrarresourceregistersz"></a><a name="resourceregistersz"></a> IRegistrar:: Ресаурцерегистерсз

Регистрирует ресурс.

```
virtual HRESULT STDMETHODCALLTYPE ResourceRegisterSz(
    /* [in] */ _In_z_ LPCOLESTR resFileName,
    /* [in] */ _In_z_ LPCOLESTR szID,
    /* [in] */ _In_z_ LPCOLESTR szType) = 0;
```

## <a name="iregistrarresourceunregistersz"></a><a name="resourceunregistersz"></a> IRegistrar:: Ресаурцеунрегистерсз

Отменяет регистрацию ресурса.

```
virtual HRESULT STDMETHODCALLTYPE ResourceUnregisterSz(
    /* [in] */ _In_z_ LPCOLESTR resFileName,
    /* [in] */ _In_z_ LPCOLESTR szID,
    /* [in] */ _In_z_ LPCOLESTR szType) = 0;
```

## <a name="iregistrarfileregister"></a><a name="fileregister"></a> IRegistrar:: Филерегистер

Регистрирует файл.

```
virtual HRESULT STDMETHODCALLTYPE FileRegister(
    /* [in] */ _In_z_ LPCOLESTR fileName) = 0;
```

## <a name="iregistrarfileunregister"></a><a name="fileunregister"></a> IRegistrar:: Филеунрегистер

Отменяет регистрацию файла.

```
virtual HRESULT STDMETHODCALLTYPE FileUnregister(
    /* [in] */ _In_z_ LPCOLESTR fileName) = 0;
```

## <a name="iregistrarstringregister"></a><a name="stringregister"></a> IRegistrar:: Стрингрегистер

Регистрирует указанные строковые данные.

```
virtual HRESULT STDMETHODCALLTYPE StringRegister(
    /* [in] */ _In_z_ LPCOLESTR data) = 0;
```

## <a name="iregistrarstringunregister"></a><a name="stringunregister"></a> IRegistrar:: Стрингунрегистер

Отменяет регистрацию указанных строковых данных.

```
virtualHRESULT STDMETHODCALLTYPE StringUnregister(
    /* [in] */ _In_z_ LPCOLESTR data) = 0;
```

## <a name="iregistrarresourceregister"></a><a name="resourceregister"></a> IRegistrar:: Ресаурцерегистер

Регистрирует ресурс.

```
virtual HRESULT STDMETHODCALLTYPE ResourceRegister(
    /* [in] */ _In_z_ LPCOLESTR resFileName,
    /* [in] */ _In_ UINT nID,
    /* [in] */ _In_z_ LPCOLESTR szType) = 0;
```

## <a name="iregistrarresourceunregister"></a><a name="resourceunregister"></a> IRegistrar:: Ресаурцеунрегистер

Отменяет регистрацию ресурса.

```
virtualHRESULT STDMETHODCALLTYPE ResourceUnregister(
    /* [in] */ _In_z_ LPCOLESTR resFileName,
    /* [in] */ _In_ UINT nID,
    /* [in] */ _In_z_ LPCOLESTR szType) = 0;
```

## <a name="see-also"></a>См. также раздел

[Использование заменяемых параметров (препроцессор регистратора)](../../atl/using-replaceable-parameters-the-registrar-s-preprocessor.md)<br/>
[Общие сведения о классах](../../atl/atl-class-overview.md)<br/>
[Классы модулей](../../atl/atl-module-classes.md)<br/>
[Компонент реестра (регистратор)](../../atl/atl-registry-component-registrar.md)
