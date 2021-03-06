---
title: IOpenRowsetImpl 類別
ms.date: 11/04/2016
f1_keywords:
- IOpenRowsetImpl
- IOpenRowsetImpl.CreateRowset
- IOpenRowsetImpl::CreateRowset
- CreateRowset
- OpenRowset
- IOpenRowsetImpl::OpenRowset
- IOpenRowsetImpl.OpenRowset
helpviewer_keywords:
- IOpenRowsetImpl class
- CreateRowset method
- OpenRowset method
ms.assetid: d259cedc-1db4-41cf-bc9f-5030907ab486
ms.openlocfilehash: 6f0dfb90b0ea79e115f459968558e48ae9827e40
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390772"
---
# <a name="iopenrowsetimpl-class"></a>IOpenRowsetImpl 類別

提供實作`IOpenRowset`介面。

## <a name="syntax"></a>語法

```cpp
template <class SessionClass>
class IOpenRowsetImpl : public IOpenRowset
```

### <a name="parameters"></a>參數

*SessionClass*<br/>
您的類別，衍生自`IOpenRowsetImpl`。

## <a name="requirements"></a>需求

**Header:** atldb.h

## <a name="members"></a>成員

### <a name="methods"></a>方法

|||
|-|-|
|[CreateRowset](#createrowset)|建立資料列集物件。 不直接由使用者呼叫。|
|[OpenRowset](#openrowset)|隨即開啟，並傳回包含單一基底資料表或索引中的所有資料列的資料列集。 （不在 ATLDB。H)|

## <a name="remarks"></a>備註

[IOpenRowset](/previous-versions/windows/desktop/ms716946(v=vs.85))介面是必要的工作階段物件。 它會開啟，並傳回包含單一基底資料表或索引中的所有資料列的資料列集。

## <a name="createrowset"></a> IOpenRowsetImpl::CreateRowset

建立資料列集物件。 不直接由使用者呼叫。 請參閱[iopenrowset:: Openrowset](/previous-versions/windows/desktop/ms716724(v=vs.85))在*OLE DB 程式設計人員參考。*

### <a name="syntax"></a>語法

```cpp
template template <class RowsetClass>
HRESULT CreateRowset(IUnknown* pUnkOuter,
   DBID* pTableID,
   DBID* pIndexID,
   REFIID riid,
   ULONG cPropertySets,
   DBPROPSET rgPropertySets[],
   IUnknown** ppRowset,
   RowsetClass*& pRowsetObj);
```

#### <a name="parameters"></a>參數

*RowsetClass*<br/>
代表使用者的資料列集類別的樣板類別成員。 通常是由精靈產生。

*pRowsetObj*<br/>
[out]資料列集物件的指標。 通常不會使用此參數，但如果您必須在資料列集上執行更多工作，再將它傳遞至 COM 物件可以使用它。 存留期*pRowsetObj*繫結*Pprowset&lt*。

其他參數，請參閱[iopenrowset:: Openrowset](/previous-versions/windows/desktop/ms716724(v=vs.85))在*OLE DB 程式設計人員參考。*

## <a name="openrowset"></a> IOpenRowsetImpl::OpenRowset

隨即開啟，並傳回包含單一基底資料表或索引中的所有資料列的資料列集。

### <a name="syntax"></a>語法

```cpp
HRESULT OpenRowset(IUnknown* pUnkOuter,
   DBID* pTableID,
   DBID* pIndexID,
   REFIID riid,
   ULONG cPropertySets,
   DBPROPSET rgPropertySets[],
   IUnknown** ppRowset);
```

#### <a name="parameters"></a>參數

請參閱[iopenrowset:: Openrowset](/previous-versions/windows/desktop/ms716724(v=vs.85))中*OLE DB 程式設計人員參考*。

### <a name="remarks"></a>備註

ATLDB 中找不到這個方法。H. 它會建立 [ATL 物件精靈] 建立提供者。

## <a name="see-also"></a>另請參閱

[OLE DB 提供者樣板](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB 提供者範本架構](../../data/oledb/ole-db-provider-template-architecture.md)