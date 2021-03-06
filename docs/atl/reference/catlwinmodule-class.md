---
title: CAtlWinModule 類別
ms.date: 11/04/2016
f1_keywords:
- CAtlWinModule
- ATLBASE/ATL::CAtlWinModule
- ATLBASE/ATL::CAtlWinModule::CAtlWinModule
- ATLBASE/ATL::CAtlWinModule::AddCreateWndData
- ATLBASE/ATL::CAtlWinModule::ExtractCreateWndData
helpviewer_keywords:
- CAtlWinModule class
ms.assetid: 7ec844af-0f68-4a34-b0c8-9de50a025df0
ms.openlocfilehash: d0bc98fa48f84e67ab38106dea3fe22d5ad1757d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62246820"
---
# <a name="catlwinmodule-class"></a>CAtlWinModule 類別

這個類別提供 ATL 視窗化元件的支援。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
class CAtlWinModule : public _ATL_WIN_MODULE
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CAtlWinModule::CAtlWinModule](#catlwinmodule)|建構函式。|
|[CAtlWinModule:: ~ CAtlWinModule](#dtor)|解構函式。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CAtlWinModule::AddCreateWndData](#addcreatewnddata)|加入資料物件。|
|[CAtlWinModule::ExtractCreateWndData](#extractcreatewnddata)|傳回視窗模組資料物件的指標。|

## <a name="remarks"></a>備註

這個類別會提供所有 ATL 類別所需的時間範圍功能的支援。

## <a name="inheritance-hierarchy"></a>繼承階層

[_ATL_WIN_MODULE](atl-typedefs.md#_atl_win_module)

`CAtlWinModule`

## <a name="requirements"></a>需求

**標頭：** atlbase.h

##  <a name="addcreatewnddata"></a>  CAtlWinModule::AddCreateWndData

這個方法會初始化，並將`_AtlCreateWndData`結構。

```
void AddCreateWndData(_AtlCreateWndData* pData, void* pObject);
```

### <a name="parameters"></a>參數

*pData*<br/>
指標`_AtlCreateWndData`會初始化並新增至目前模組的結構。

*pObject*<br/>
物件的指標**這**指標。

### <a name="remarks"></a>備註

這個方法會呼叫[AtlWinModuleAddCreateWndData](winmodule-global-functions.md#atlwinmoduleaddcreatewnddata)哪些初始化[_AtlCreateWndData](../../atl/reference/atlcreatewnddata-structure.md)結構。 此結構會儲存**這**指標，用來取得視窗程序中的類別執行個體。

##  <a name="catlwinmodule"></a>  CAtlWinModule::CAtlWinModule

建構函式。

```
CAtlWinModule();
```

### <a name="remarks"></a>備註

如果初始化失敗， **EXCEPTION_NONCONTINUABLE**引發的例外狀況。

##  <a name="dtor"></a>  CAtlWinModule:: ~ CAtlWinModule

解構函式。

```
~CAtlWinModule();
```

### <a name="remarks"></a>備註

釋放所有配置的資源。

##  <a name="extractcreatewnddata"></a>  CAtlWinModule::ExtractCreateWndData

這個方法傳回的指標`_AtlCreateWndData`結構。

```
void* ExtractCreateWndData();
```

### <a name="return-value"></a>傳回值

將指標傳回至`_AtlCreateWndData`結構之前加[CAtlWinModule::AddCreateWndData](#addcreatewnddata)，或如果沒有物件，則為 NULL。

## <a name="see-also"></a>另請參閱

[_ATL_WIN_MODULE](atl-typedefs.md#_atl_win_module)<br/>
[類別概觀](../../atl/atl-class-overview.md)<br/>
[模組類別](../../atl/atl-module-classes.md)
