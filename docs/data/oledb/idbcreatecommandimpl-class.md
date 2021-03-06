---
title: IDBCreateCommandImpl 類別
ms.date: 11/04/2016
f1_keywords:
- ATL::IDBCreateCommandImpl
- IDBCreateCommandImpl
- ATL.IDBCreateCommandImpl
- IDBCreateCommandImpl.CreateCommand
- CreateCommand
- IDBCreateCommandImpl::CreateCommand
helpviewer_keywords:
- IDBCreateCommandImpl class
- CreateCommand method
ms.assetid: eac4755e-1668-42e1-958e-a35620c385ae
ms.openlocfilehash: 7450d91cd5e5383b55e2ebb391fe5f1190cbed2a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62408910"
---
# <a name="idbcreatecommandimpl-class"></a>IDBCreateCommandImpl 類別

提供實作[IDBCreateCommand](/previous-versions/windows/desktop/ms711625(v=vs.85))介面。

## <a name="syntax"></a>語法

```cpp
template <class T, class CommandClass >
class ATL_NO_VTABLE IDBCreateCommandImpl
   : public IDBCreateCommand
```

### <a name="parameters"></a>參數

*T*<br/>
工作階段物件衍生自`IDBCreateCommandImpl`。

*CommandClass*<br/>
您的命令類別。

## <a name="requirements"></a>需求

**Header:** atldb.h

## <a name="members"></a>成員

### <a name="interface-methods"></a>介面方法

|||
|-|-|
|[CreateCommand](#createcommand)|建立新的命令。|

## <a name="remarks"></a>備註

若要取得新的命令的工作階段物件上選擇性的介面。

## <a name="createcommand"></a> IDBCreateCommandImpl::CreateCommand

建立新的命令，並傳回要求的介面。

### <a name="syntax"></a>語法

```cpp
STDMETHOD(CreateCommand)(IUnknown * pUnkOuter,
   REFIID riid,
   IUnknown ** ppvCommand);
```

#### <a name="parameters"></a>參數

請參閱[idbcreatecommand:: Createcommand](/previous-versions/windows/desktop/ms709772(v=vs.85))中*OLE DB 程式設計人員參考*。

某些參數會對應至*OLE DB 程式設計人員參考*參數中所述的不同名稱的`IDBCreateCommand::CreateCommand`:

|OLE DB 範本參數|*OLE DB 程式設計人員參考*參數|
|--------------------------------|------------------------------------------------|
|*ppvCommand*|*ppCommand*|

## <a name="see-also"></a>另請參閱

[OLE DB 提供者樣板](../../data/oledb/ole-db-provider-templates-cpp.md)<br/>
[OLE DB 提供者範本架構](../../data/oledb/ole-db-provider-template-architecture.md)