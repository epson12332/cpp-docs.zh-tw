---
title: IDataObjectImpl 類別
ms.date: 11/04/2016
f1_keywords:
- IDataObjectImpl
- ATLCTL/ATL::IDataObjectImpl
- ATLCTL/ATL::IDataObjectImpl::DAdvise
- ATLCTL/ATL::IDataObjectImpl::DUnadvise
- ATLCTL/ATL::IDataObjectImpl::EnumDAdvise
- ATLCTL/ATL::IDataObjectImpl::EnumFormatEtc
- ATLCTL/ATL::IDataObjectImpl::FireDataChange
- ATLCTL/ATL::IDataObjectImpl::GetCanonicalFormatEtc
- ATLCTL/ATL::IDataObjectImpl::GetData
- ATLCTL/ATL::IDataObjectImpl::GetDataHere
- ATLCTL/ATL::IDataObjectImpl::QueryGetData
- ATLCTL/ATL::IDataObjectImpl::SetData
helpviewer_keywords:
- data transfer [C++]
- data transfer [C++], Uniform Data Transfer
- IDataObjectImpl class
- IDataObject, ATL implementation
ms.assetid: b680f0f7-7795-40a1-a0f6-f48768201c89
ms.openlocfilehash: b73cfe83075b9595bc98ca05ab2ec2e1771a038d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62275460"
---
# <a name="idataobjectimpl-class"></a>IDataObjectImpl 類別

這個類別提供方法來支援制式資料傳輸及管理連線。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template<class T>
class IDataObjectImpl
```

#### <a name="parameters"></a>參數

*T*<br/>
您的類別，衍生自`IDataObjectImpl`。

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[IDataObjectImpl::DAdvise](#dadvise)|建立資料物件和通知接收之間的連線。 這可讓通知接收物件中接收通知的變更。|
|[IDataObjectImpl::DUnadvise](#dunadvise)|會透過先前建立的連線終止`DAdvise`。|
|[IDataObjectImpl::EnumDAdvise](#enumdadvise)|建立列舉值以逐一查看目前的諮詢連接。|
|[IDataObjectImpl::EnumFormatEtc](#enumformatetc)|建立列舉值以逐一查看`FORMATETC`資料物件所支援的結構。 ATL 實作會傳回 E_NOTIMPL。|
|[IDataObjectImpl::FireDataChange](#firedatachange)|將變更通知傳回給每個通知的接收。|
|[IDataObjectImpl::GetCanonicalFormatEtc](#getcanonicalformatetc)|擷取邏輯上等同`FORMATETC`到另一個則是更複雜的結構。 ATL 實作會傳回 E_NOTIMPL。|
|[IDataObjectImpl::GetData](#getdata)|將資料從資料物件傳輸至用戶端。 資料所述`FORMATETC`結構，並透過傳輸`STGMEDIUM`結構。|
|[IDataObjectImpl::GetDataHere](#getdatahere)|類似於`GetData`，但用戶端必須配置`STGMEDIUM`結構。 ATL 實作會傳回 E_NOTIMPL。|
|[IDataObjectImpl::QueryGetData](#querygetdata)|判斷資料物件是否支援特定`FORMATETC`傳輸資料的結構。 ATL 實作會傳回 E_NOTIMPL。|
|[IDataObjectImpl::SetData](#setdata)|將資料從用戶端傳輸至資料物件。 ATL 實作會傳回 E_NOTIMPL。|

## <a name="remarks"></a>備註

[IDataObject](/windows/desktop/api/objidl/nn-objidl-idataobject)介面提供方法來支援制式資料傳輸。 `IDataObject` 使用標準的格式結構[FORMATETC](/windows/desktop/api/objidl/ns-objidl-tagformatetc)並[STGMEDIUM](/windows/desktop/api/objidl/ns-objidl-tagstgmedium)來擷取與儲存資料。

`IDataObject` 也會管理通知來處理資料變更通知接收的連接。 為了讓用戶端收到的資料物件中的資料變更通知，用戶端必須實作[IAdviseSink](/windows/desktop/api/objidl/nn-objidl-iadvisesink)物件呼叫通知接收上的介面。 當用戶端接著呼叫`IDataObject::DAdvise`，資料物件和通知接收之間建立連線。

類別`IDataObjectImpl`提供的預設實作`IDataObject`並實作`IUnknown`資訊傳送給傾印裝置在偵錯組建。

**相關文章** [ATL 教學課程](../../atl/active-template-library-atl-tutorial.md)，[建立 ATL 專案](../../atl/reference/creating-an-atl-project.md)

## <a name="inheritance-hierarchy"></a>繼承階層

`IDataObject`

`IDataObjectImpl`

## <a name="requirements"></a>需求

**標頭：** atlctl.h

##  <a name="dadvise"></a>  IDataObjectImpl::DAdvise

建立資料物件和通知接收之間的連線。

```
HRESULT DAdvise(
    FORMATETC* pformatetc,
    DWORD advf,
    IAdviseSink* pAdvSink,
    DWORD* pdwConnection);
```

### <a name="remarks"></a>備註

這可讓通知接收物件中接收通知的變更。

若要終止的連接，呼叫[DUnadvise](#dunadvise)。

請參閱[IDataObject::DAdvise](/windows/desktop/api/objidl/nf-objidl-idataobject-dadvise) Windows SDK 中。

##  <a name="dunadvise"></a>  IDataObjectImpl::DUnadvise

會透過先前建立的連線終止[DAdvise](#dadvise)。

```
HRESULT DUnadvise(DWORD dwConnection);
```

### <a name="remarks"></a>備註

請參閱[IDataObject::DUnadvise](/windows/desktop/api/objidl/nf-objidl-idataobject-dunadvise) Windows SDK 中。

##  <a name="enumdadvise"></a>  IDataObjectImpl::EnumDAdvise

建立列舉值以逐一查看目前的諮詢連接。

```
HRESULT DAdvise(
    FORMATETC* pformatetc,
    DWORD advf,
    IAdviseSink* pAdvSink,
    DWORD* pdwConnection);
```

### <a name="remarks"></a>備註

請參閱[IDataObject::EnumDAdvise](/windows/desktop/api/objidl/nf-objidl-idataobject-enumdadvise) Windows SDK 中。

##  <a name="enumformatetc"></a>  IDataObjectImpl::EnumFormatEtc

建立列舉值以逐一查看`FORMATETC`資料物件所支援的結構。

```
HRESULT EnumFormatEtc(
    DWORD dwDirection,
    IEnumFORMATETC** ppenumFormatEtc);
```

### <a name="remarks"></a>備註

請參閱[IDataObject::EnumFormatEtc](/windows/desktop/api/objidl/nf-objidl-idataobject-enumformatetc) Windows SDK 中。

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

##  <a name="firedatachange"></a>  IDataObjectImpl::FireDataChange

傳送回到受目前每個通知接收的變更通知。

```
HRESULT FireDataChange();
```

### <a name="return-value"></a>傳回值

標準的 HRESULT 值。

##  <a name="getcanonicalformatetc"></a>  IDataObjectImpl::GetCanonicalFormatEtc

擷取邏輯上等同`FORMATETC`到另一個則是更複雜的結構。

```
HRESULT GetCanonicalFormatEtc(FORMATETC* pformatetcIn, FORMATETC* pformatetcOut);
```

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

### <a name="remarks"></a>備註

請參閱[IDataObject::GetCanonicalFormatEtc](/windows/desktop/api/objidl/nf-objidl-idataobject-getcanonicalformatetc) Windows SDK 中。

##  <a name="getdata"></a>  IDataObjectImpl::GetData

將資料從資料物件傳輸至用戶端。

```
HRESULT GetData(
    FORMATETC* pformatetcIn,
    STGMEDIUM* pmedium);
```

### <a name="remarks"></a>備註

*PformatetcIn*參數必須指定 TYMED_MFPICT 的儲存媒體類型。

請參閱[idataobject:: Getdata](/windows/desktop/api/objidl/nf-objidl-idataobject-getdata) Windows SDK 中。

##  <a name="getdatahere"></a>  IDataObjectImpl::GetDataHere

類似於`GetData`，但用戶端必須配置`STGMEDIUM`結構。

```
HRESULT GetDataHere(
    FORMATETC* pformatetc,
    STGMEDIUM* pmedium);
```

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

### <a name="remarks"></a>備註

請參閱[IDataObject::GetDataHere](/windows/desktop/api/objidl/nf-objidl-idataobject-getdatahere) Windows SDK 中。

##  <a name="querygetdata"></a>  IDataObjectImpl::QueryGetData

判斷資料物件是否支援特定`FORMATETC`傳輸資料的結構。

```
HRESULT QueryGetData(FORMATETC* pformatetc);
```

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

### <a name="remarks"></a>備註

請參閱[IDataObject::QueryGetData](/windows/desktop/api/objidl/nf-objidl-idataobject-querygetdata) Windows SDK 中。

##  <a name="setdata"></a>  IDataObjectImpl::SetData

將資料從用戶端傳輸至資料物件。

```
HRESULT SetData(
    FORMATETC* pformatetc,
    STGMEDIUM* pmedium,
    BOOL fRelease);
```

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

### <a name="remarks"></a>備註

請參閱[IDataObject::SetData](/windows/desktop/api/objidl/nf-objidl-idataobject-setdata) Windows SDK 中。

## <a name="see-also"></a>另請參閱

[類別概觀](../../atl/atl-class-overview.md)
