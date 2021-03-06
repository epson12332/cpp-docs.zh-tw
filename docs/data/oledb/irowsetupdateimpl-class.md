---
title: IRowsetUpdateImpl 類別
ms.date: 11/04/2016
f1_keywords:
- IRowsetUpdateImpl
- ATL.IRowsetUpdateImpl
- ATL::IRowsetUpdateImpl
- SetData
- IRowsetUpdateImpl::SetData
- IRowsetUpdateImpl.SetData
- ATL::IRowsetUpdateImpl::SetData
- ATL.IRowsetUpdateImpl.SetData
- ATL.IRowsetUpdateImpl.GetOriginalData
- IRowsetUpdateImpl.GetOriginalData
- GetOriginalData
- ATL::IRowsetUpdateImpl::GetOriginalData
- IRowsetUpdateImpl::GetOriginalData
- IRowsetUpdateImpl::GetPendingRows
- GetPendingRows
- IRowsetUpdateImpl.GetPendingRows
- ATL::IRowsetUpdateImpl::GetPendingRows
- ATL.IRowsetUpdateImpl.GetPendingRows
- ATL.IRowsetUpdateImpl.GetRowStatus
- IRowsetUpdateImpl::GetRowStatus
- IRowsetUpdateImpl.GetRowStatus
- ATL::IRowsetUpdateImpl::GetRowStatus
- GetRowStatus
- ATL.IRowsetUpdateImpl.Undo
- ATL::IRowsetUpdateImpl::Undo
- IRowsetUpdateImpl::Undo
- IRowsetUpdateImpl.Undo
- ATL::IRowsetUpdateImpl::Update
- IRowsetUpdateImpl::Update
- IRowsetUpdateImpl.Update
- ATL.IRowsetUpdateImpl.Update
- IRowsetUpdateImpl::IsUpdateAllowed
- IRowsetUpdateImpl.IsUpdateAllowed
- IsUpdateAllowed
- IRowsetUpdateImpl.m_mapCachedData
- IRowsetUpdateImpl::m_mapCachedData
- m_mapCachedData
helpviewer_keywords:
- providers, updatable
- IRowsetUpdateImpl class
- updatable providers, deferred update
- SetData method
- GetOriginalData method
- GetPendingRows method
- GetRowStatus method
- Undo method
- Update method
- IsUpdateAllowed method
- m_mapCachedData
ms.assetid: f85af76b-ab6f-4f8b-8f4a-337c9679d68f
ms.openlocfilehash: 6c20698e2219cf7c3e1d840e23b5f8113947ae9f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390700"
---
# <a name="irowsetupdateimpl-class"></a>IRowsetUpdateImpl 類別

OLE DB 樣板實作[IRowsetUpdate](/previous-versions/windows/desktop/ms714401(v=vs.85))介面。

## <a name="syntax"></a>語法

```cpp
template <
   class T,
   class Storage,
   class UpdateArray = CAtlArray<Storage>,
   class RowClass = CSimpleRow,
   class MapClass = CAtlMap <RowClass::KeyType, RowClass*>
>

class IRowsetUpdateImpl : public IRowsetChangeImpl<
   T,
   Storage,
   IRowsetUpdate,
   RowClass,
   MapClass>
```

### <a name="parameters"></a>參數

*T*<br/>
類別衍生自`IRowsetUpdateImpl`。

*儲存體*<br/>
使用者記錄中。

*UpdateArray*<br/>
陣列，包含更新資料列集快取的資料。

*RowClass*<br/>
儲存體單位`HROW`。

*MapClass*<br/>
提供者所持有的所有資料列控制代碼儲存體單位。

## <a name="requirements"></a>需求

**Header:** atldb.h

## <a name="members"></a>成員

### <a name="interface-methods-used-with-irowsetchange"></a>（搭配 IRowsetChange） 的介面方法

|||
|-|-|
|[SetData](#setdata)|設定一或多個資料行中的資料值。|

### <a name="interface-methods-used-with-irowsetupdate"></a>（搭配 IRowsetUpdate） 的介面方法

|||
|-|-|
|[GetOriginalData](#getoriginaldata)|取得最近傳送至或從資料來源，略過暫止的變更取得的資料。|
|[GetPendingRows](#getpendingrows)|傳回一份具有暫止的變更的資料列。|
|[GetRowStatus](#getrowstatus)|傳回指定的資料列的狀態。|
|[復原](#undo)|復原自上次擷取或更新的資料列的任何變更。|
|[更新](#update)|會傳輸自上次擷取或更新資料列所做的變更。|

### <a name="implementation-methods-callback"></a>實作方法 （回呼）

|||
|-|-|
|[IsUpdateAllowed](#isupdateallowed)|用來檢查安全性，完整性，依此類推之前允許更新。|

### <a name="data-members"></a>資料成員

|||
|-|-|
|[m_mapCachedData](#mapcacheddata)|包含原始資料延遲的作業。|

## <a name="remarks"></a>備註

您應該先閱讀，並了解的文件[IRowsetChange](/previous-versions/windows/desktop/ms715790(v=vs.85))，因為這裡所述的所有項目也適用於此處。 您也應該閱讀的第 6 章*OLE DB 程式設計人員參考*上設定資料。

`IRowsetUpdateImpl` 實作 OLE DB`IRowsetUpdate`介面，讓消費者可以延遲的具有所做的變更傳輸`IRowsetChange`到資料來源，並復原變更，才能加以傳送。

> [!IMPORTANT]
>  強烈建議您先閱讀下列文件，然後再嘗試實作您的提供者：

- [建立可更新的提供者](../../data/oledb/creating-an-updatable-provider.md)

- 第 6 章*OLE DB 程式設計人員參考*

- 另請參閱如何`RUpdateRowset`類別用於[UpdatePV](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/ATL/OLEDB/Provider/UPDATEPV)範例

## <a name="setdata"></a> IRowsetUpdateImpl::SetData

設定一或多個資料行中的資料值。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (SetData )(HROW hRow,
   HACCESSOR hAccessor,
   void* pSrcData);
```

#### <a name="parameters"></a>參數

請參閱[irowsetchange:: Setdata](/previous-versions/windows/desktop/ms721232(v=vs.85))中*OLE DB 程式設計人員參考*。

### <a name="remarks"></a>備註

這個方法會覆寫[irowsetchangeimpl:: Setdata](../../data/oledb/irowsetchangeimpl-setdata.md)方法，但包含原始資料，以允許立即或延後在處理作業的快取。

## <a name="getoriginaldata"></a> IRowsetUpdateImpl::GetOriginalData

取得最近傳送至或從資料來源，略過暫止的變更取得的資料。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (GetOriginalData )(HROW hRow,
   HACCESSOR hAccessor,
   void* pData);
```

#### <a name="parameters"></a>參數

請參閱[IRowsetUpdate::GetOriginalData](/previous-versions/windows/desktop/ms709947(v=vs.85))中*OLE DB 程式設計人員參考*。

## <a name="getpendingrows"></a> IRowsetUpdateImpl::GetPendingRows

傳回一份具有暫止的變更的資料列。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (GetPendingRows )(HCHAPTER /* hReserved */,
   DBPENDINGSTATUS dwRowStatus,
   DBCOUNTITEM* pcPendingRows,
   HROW** prgPendingRows,
   DBPENDINGSTATUS** prgPendingStatus);
```

#### <a name="parameters"></a>參數

*hReserved*<br/>
[in]對應至*hChapter*中的參數[IRowsetUpdate::GetPendingRows](/previous-versions/windows/desktop/ms719626(v=vs.85))。

其他參數，請參閱[IRowsetUpdate::GetPendingRows](/previous-versions/windows/desktop/ms719626(v=vs.85))中*OLE DB 程式設計人員參考*。

### <a name="remarks"></a>備註

如需詳細資訊，請參閱 < [IRowsetUpdate::GetPendingRows](/previous-versions/windows/desktop/ms719626(v=vs.85))中*OLE DB 程式設計人員參考*。

## <a name="getrowstatus"></a> IRowsetUpdateImpl::GetRowStatus

傳回指定的資料列的狀態。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (GetRowStatus )(HCHAPTER /* hReserved */,
   DBCOUNTITEM cRows,
   const HROW rghRows[],
   DBPENDINGSTATUS rgPendingStatus[]);
```

#### <a name="parameters"></a>參數

*hReserved*<br/>
[in]對應至*hChapter*中的參數[IRowsetUpdate::GetRowStatus](/previous-versions/windows/desktop/ms724377(v=vs.85))。

其他參數，請參閱[IRowsetUpdate::GetRowStatus](/previous-versions/windows/desktop/ms724377(v=vs.85))中*OLE DB 程式設計人員參考*。

## <a name="undo"></a> IRowsetUpdateImpl::Undo

復原自上次擷取或更新的資料列的任何變更。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (Undo )(HCHAPTER /* hReserved */,
   DBCOUNTITEM cRows,
   const HROW rghRows[ ],
   DBCOUNTITEM* pcRowsUndone,
   HROW** prgRowsUndone,
   DBROWSTATUS** prgRowStatus);
```

#### <a name="parameters"></a>參數

*hReserved*<br/>
[in]對應至*hChapter*中的參數[IRowsetUpdate::Undo](/previous-versions/windows/desktop/ms719655(v=vs.85))。

*pcRowsUndone*<br/>
[out]對應至*pcRows*中的參數[IRowsetUpdate::Undo](/previous-versions/windows/desktop/ms719655(v=vs.85))。

*prgRowsUndone*<br/>
[in]對應至*prgRows*中的參數[IRowsetUpdate::Undo](/previous-versions/windows/desktop/ms719655(v=vs.85))。

其他參數，請參閱[IRowsetUpdate::Undo](/previous-versions/windows/desktop/ms719655(v=vs.85))中*OLE DB 程式設計人員參考*。

## <a name="update"></a> IRowsetUpdateImpl::Update

會傳輸自上次擷取或更新資料列所做的變更。

### <a name="syntax"></a>語法

```cpp
STDMETHOD (Update )(HCHAPTER /* hReserved */,
   DBCOUNTITEM cRows,
   const HROW rghRows[],
   DBCOUNTITEM* pcRows,
   HROW** prgRows,
   DBROWSTATUS** prgRowStatus);
```

#### <a name="parameters"></a>參數

*hReserved*<br/>
[in]對應至*hChapter*中的參數[irowsetupdate:: Update](/previous-versions/windows/desktop/ms719709(v=vs.85))。

其他參數，請參閱[irowsetupdate:: Update](/previous-versions/windows/desktop/ms719709(v=vs.85))中*OLE DB 程式設計人員參考*。

### <a name="remarks"></a>備註

變更傳輸藉由呼叫[irowsetchangeimpl:: Flushdata](../../data/oledb/irowsetchangeimpl-flushdata.md)。 取用者必須呼叫[Crowset](../../data/oledb/crowset-update.md) ，變更才會生效。 設定*Prgrowstatus&lt*設為適當的值中所述[資料列狀態](/previous-versions/windows/desktop/ms722752(v=vs.85))中*OLE DB 程式設計人員參考*。

## <a name="isupdateallowed"></a> IRowsetUpdateImpl::IsUpdateAllowed

覆寫此方法來檢查安全性，完整性，在更新之前，依此類推。

### <a name="syntax"></a>語法

```cpp
HRESULT IsUpdateAllowed(DBPENDINGSTATUS /* [in] */ /* status */,
   HROW /* [in] */ /* hRowUpdate */,
   DBROWSTATUS* /* [out] */ /* pRowStatus */);
```

#### <a name="parameters"></a>參數

*status*<br/>
[in]暫止的資料列上的作業的狀態。

*hRowUpdate*<br/>
[in]使用者想要更新的資料列的控制代碼。

*pRowStatus*<br/>
[out]傳回給使用者的狀態。

### <a name="remarks"></a>備註

如果您判斷，應該允許更新，會傳回 S_OK;否則會傳回 E_FAIL。 如果您允許更新，您也需要設定`DBROWSTATUS`中[irowsetupdateimpl:: Update](../../data/oledb/irowsetupdateimpl-update.md)適當[資料列狀態](/previous-versions/windows/desktop/ms722752(v=vs.85))。

## <a name="mapcacheddata"></a> IRowsetUpdateImpl::m_mapCachedData

對應，其包含延遲作業的原始資料。

### <a name="syntax"></a>語法

```cpp
CAtlMap<
   HROW hRow, 
   Storage* pData
>
m_mapCachedData;
```

#### <a name="parameters"></a>參數

*hRow*<br/>
資料的資料列的控制代碼。

*pData*<br/>
快取資料的指標。 資料是類型*儲存體*（使用者記錄類別）。 請參閱*儲存體*中的範本引數[IRowsetUpdateImpl 類別](../../data/oledb/irowsetupdateimpl-class.md)。

## <a name="see-also"></a>另請參閱

[OLE DB 提供者樣板](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB 提供者範本架構](../../data/oledb/ole-db-provider-template-architecture.md)<br/>
[建立可更新的提供者](../../data/oledb/creating-an-updatable-provider.md)