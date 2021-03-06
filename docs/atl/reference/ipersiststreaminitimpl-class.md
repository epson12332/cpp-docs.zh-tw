---
title: IPersistStreamInitImpl 類別
ms.date: 11/04/2016
f1_keywords:
- IPersistStreamInitImpl
- ATLCOM/ATL::IPersistStreamInitImpl
- ATLCOM/ATL::IPersistStreamInitImpl::GetClassID
- ATLCOM/ATL::IPersistStreamInitImpl::GetSizeMax
- ATLCOM/ATL::IPersistStreamInitImpl::InitNew
- ATLCOM/ATL::IPersistStreamInitImpl::IsDirty
- ATLCOM/ATL::IPersistStreamInitImpl::Load
- ATLCOM/ATL::IPersistStreamInitImpl::Save
helpviewer_keywords:
- IPersistStreamInit ATL implementation
- IPersistStreamInitImpl class
- streams, ATL
ms.assetid: ef217c3c-020f-4cf8-871e-ef68e57865b8
ms.openlocfilehash: b5ab433ed08b150e6c344d65657a910542856e77
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62197615"
---
# <a name="ipersiststreaminitimpl-class"></a>IPersistStreamInitImpl 類別

這個類別會實作`IUnknown`，並提供的預設實作[IPersistStreamInit](/windows/desktop/api/ocidl/nn-ocidl-ipersiststreaminit)介面。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template<class T>
class ATL_NO_VTABLE IPersistStreamInitImpl
   : public IPersistStreamInit
```

#### <a name="parameters"></a>參數

*T*<br/>
您的類別，衍生自`IPersistStreamInitImpl`。

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[IPersistStreamInitImpl::GetClassID](#getclassid)|擷取物件的 CLSID。|
|[IPersistStreamInitImpl::GetSizeMax](#getsizemax)|擷取儲存物件的資料所需的資料流的大小。 ATL 實作會傳回 E_NOTIMPL。|
|[IPersistStreamInitImpl::InitNew](#initnew)|初始化新建立的物件。|
|[IPersistStreamInitImpl::IsDirty](#isdirty)|會檢查自上次儲存後，是否已變更物件的資料。|
|[IPersistStreamInitImpl::Load](#load)|從指定的資料流載入物件的屬性。|
|[IPersistStreamInitImpl::Save](#save)|將指定的資料流物件的屬性。|

## <a name="remarks"></a>備註

[IPersistStreamInit](/windows/desktop/api/ocidl/nn-ocidl-ipersiststreaminit)介面可讓用戶端要求載入您的物件，並將其持續性資料儲存至單一資料流。 類別`IPersistStreamInitImpl`提供此介面的預設實作，並實作`IUnknown`資訊傳送給傾印裝置在偵錯組建。

**相關文章** [ATL 教學課程](../../atl/active-template-library-atl-tutorial.md)，[建立 ATL 專案](../../atl/reference/creating-an-atl-project.md)

## <a name="inheritance-hierarchy"></a>繼承階層

`IPersistStreamInit`

`IPersistStreamInitImpl`

## <a name="requirements"></a>需求

**標頭：** atlcom.h

##  <a name="getclassid"></a>  IPersistStreamInitImpl::GetClassID

擷取物件的 CLSID。

```
STDMETHOD(GetClassID)(CLSID* pClassID);
```

### <a name="remarks"></a>備註

請參閱[IPersist::GetClassID](/windows/desktop/api/objidl/nf-objidl-ipersist-getclassid) Windows SDK 中。

##  <a name="getsizemax"></a>  IPersistStreamInitImpl::GetSizeMax

擷取儲存物件的資料所需的資料流的大小。

```
STDMETHOD(GetSizeMax)(ULARGE_INTEGER FAR* pcbSize);
```

### <a name="return-value"></a>傳回值

傳回 E_NOTIMPL。

### <a name="remarks"></a>備註

請參閱[IPersistStreamInit::GetSizeMax](/windows/desktop/api/ocidl/nf-ocidl-ipersiststreaminit-getsizemax) Windows SDK 中。

##  <a name="initnew"></a>  IPersistStreamInitImpl::InitNew

初始化新建立的物件。

```
STDMETHOD(InitNew)();
```

### <a name="remarks"></a>備註

請參閱[IPersistStreamInit::InitNew](/windows/desktop/api/ocidl/nf-ocidl-ipersiststreaminit-initnew) Windows SDK 中。

##  <a name="isdirty"></a>  IPersistStreamInitImpl::IsDirty

會檢查自上次儲存後，是否已變更物件的資料。

```
STDMETHOD(IsDirty)();
```

### <a name="remarks"></a>備註

請參閱[IPersistStreamInit::IsDirty](/windows/desktop/api/ocidl/nf-ocidl-ipersiststreaminit-isdirty) Windows SDK 中。

##  <a name="load"></a>  IPersistStreamInitImpl::Load

從指定的資料流載入物件的屬性。

```
STDMETHOD(Load)(LPSTREAM pStm);
```

### <a name="remarks"></a>備註

ATL 會使用物件的屬性對應，來擷取這項資訊。

請參閱[IPersistStreamInit::Load](/windows/desktop/api/ocidl/nf-ocidl-ipersiststreaminit-load) Windows SDK 中。

##  <a name="save"></a>  IPersistStreamInitImpl::Save

將指定的資料流物件的屬性。

```
STDMETHOD(Save)(LPSTREAM pStm, BOOL fClearDirty);
```

### <a name="remarks"></a>備註

ATL 會使用物件的屬性對應來儲存這項資訊。

請參閱[IPersistStreamInit::Save](/windows/desktop/api/ocidl/nf-ocidl-ipersiststreaminit-save) Windows SDK 中。

## <a name="see-also"></a>另請參閱

[儲存體和資料流](/windows/desktop/Stg/storages-and-streams)<br/>
[類別概觀](../../atl/atl-class-overview.md)
