---
title: IRowsetCreatorImpl 類別
ms.date: 11/04/2016
f1_keywords:
- ATL::IRowsetCreatorImpl
- ATL.IRowsetCreatorImpl
- ATL::IRowsetCreatorImpl<T>
- ATL.IRowsetCreatorImpl<T>
- IRowsetCreatorImpl
- IRowsetCreatorImpl.SetSite
- IRowsetCreatorImpl<T>::SetSite
- IRowsetCreatorImpl::SetSite
- SetSite
- ATL.IRowsetCreatorImpl.SetSite
- ATL::IRowsetCreatorImpl<T>::SetSite
- ATL::IRowsetCreatorImpl::SetSite
- ATL.IRowsetCreatorImpl<T>.SetSite
helpviewer_keywords:
- IRowsetCreatorImpl class
- SetSite method
ms.assetid: 92cc950f-7978-4754-8d9a-defa63867d82
ms.openlocfilehash: 3dc5cb06b3eb7f01667e4e1ec09dd60f9befae77
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390785"
---
# <a name="irowsetcreatorimpl-class"></a>IRowsetCreatorImpl 類別

執行相同的功能`IObjectWithSite`但也可讓 OLE DB 屬性`DBPROPCANSCROLLBACKWARDS DBPROPCANFETCHBACKWARDS`。

## <a name="syntax"></a>語法

```cpp
template < class T >
class ATL_NO_VTABLE IRowsetCreatorImpl
   : public IObjectWithSiteImpl< T >
```

### <a name="parameters"></a>參數

*T*<br/>
類別衍生自`IRowsetCreator`。

## <a name="requirements"></a>需求

**Header:** atldb.h

## <a name="members"></a>成員

### <a name="methods"></a>方法

|||
|-|-|
|[SetSite](#setsite)|設定站台，其中包含資料列集物件。|

## <a name="remarks"></a>備註

這個類別繼承自[IObjectWithSite](/windows/desktop/api/ocidl/nn-ocidl-iobjectwithsite) ，並覆寫[IObjectWithSite::SetSite](/windows/desktop/api/ocidl/nf-ocidl-iobjectwithsite-setsite)。 當提供者命令或工作階段物件會建立一個資料列集時，它會呼叫`QueryInterface`尋找資料列集物件上`IObjectWithSite`，並呼叫`SetSite`傳遞資料列集物件的`IUnkown`站介面的介面。

## <a name="setsite"></a> IRowsetCreatorImpl::SetSite

設定站台，其中包含資料列集物件。 如需詳細資訊，請參閱 < [IObjectWithSite::SetSite](/windows/desktop/api/ocidl/nf-ocidl-iobjectwithsite-setsite)。

### <a name="syntax"></a>語法

```cpp
STDMETHOD(SetSite )(IUnknown* pCreator);
```

#### <a name="parameters"></a>參數

*pCreator*<br/>
[in]指標`IUnknown`的站台管理的資料列集物件介面指標。

### <a name="return-value"></a>傳回值

標準的 HRESULT。

### <a name="remarks"></a>備註

颾魤 ㄛ`IRowsetCreatorImpl::SetSite`可讓 OLE DB`DBPROPCANSCROLLBACKWARDS DBPROPCANFETCHBACKWARDS`屬性。

## <a name="see-also"></a>另請參閱

[OLE DB 提供者樣板](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB 提供者範本架構](../../data/oledb/ole-db-provider-template-architecture.md)