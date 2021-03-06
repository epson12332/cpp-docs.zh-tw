---
title: CAtlAutoThreadModule 類別
ms.date: 11/04/2016
f1_keywords:
- CAtlAutoThreadModule
- atlbase/ATL::CAtlAutoThreadModule
helpviewer_keywords:
- CAtlAutoThreadModule class
ms.assetid: 3be834aa-55ef-403e-94ae-41979691b15f
ms.openlocfilehash: 1ec66bf77d8dd705cb2e1e93f70a885ab96420a6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62247288"
---
# <a name="catlautothreadmodule-class"></a>CAtlAutoThreadModule 類別

這個類別會實作在執行緒集區的 apartment model COM 伺服器。

> [!IMPORTANT]
> 此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
class CAtlAutoThreadModule : public CAtlAutoThreadModuleT<CAtlAutoThreadModule>
```

## <a name="remarks"></a>備註

`CAtlAutoThreadModule` 衍生自[CAtlAutoThreadModuleT](../../atl/reference/catlautothreadmodulet-class.md)並實作在執行緒集區的 apartment model COM 伺服器。 `CAtlAutoThreadModule` 會使用[CComApartment](../../atl/reference/ccomapartment-class.md)管理模組中的每個執行緒的 apartment。

您必須使用[DECLARE_CLASSFACTORY_AUTO_THREAD](aggregation-and-class-factory-macros.md#declare_classfactory_auto_thread)中指定的物件的類別定義的巨集[CComClassFactoryAutoThread](../../atl/reference/ccomclassfactoryautothread-class.md)做為 class factory。 接著，您應該加入衍生自的類別的單一執行個體`CAtlAutoThreadModuleT`這類`CAtlAutoThreadModule`。 例如: 

`CAtlAutoThreadModule _AtlAutoModule; // name is immaterial.`

> [!NOTE]
> 這個類別會取代過時[CComAutoThreadModule](../../atl/reference/ccomautothreadmodule-class.md)類別。

## <a name="inheritance-hierarchy"></a>繼承階層

`IAtlAutoThreadModule`

[CAtlAutoThreadModuleT](../../atl/reference/catlautothreadmodulet-class.md)

`CAtlAutoThreadModule`

## <a name="requirements"></a>需求

**標頭：** atlbase.h

## <a name="see-also"></a>另請參閱

[CAtlAutoThreadModuleT 類別](../../atl/reference/catlautothreadmodulet-class.md)<br/>
[IAtlAutoThreadModule 類別](../../atl/reference/iatlautothreadmodule-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)<br/>
[模組類別](../../atl/atl-module-classes.md)
