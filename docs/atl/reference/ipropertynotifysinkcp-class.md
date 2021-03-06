---
title: IPropertyNotifySinkCP 類別
ms.date: 11/04/2016
f1_keywords:
- IPropertyNotifySinkCP
- atlctl/ATL::IPropertyNotifySinkCP
helpviewer_keywords:
- connection points [C++], managing
- sinks, notifying of changes
- IPropertyNotifySinkCP class
ms.assetid: 1b41445e-bc88-4fa6-bb62-d68aacec2bd5
ms.openlocfilehash: b96e5345923d04de74dace173a80b8c4d3ee917f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62197886"
---
# <a name="ipropertynotifysinkcp-class"></a>IPropertyNotifySinkCP 類別

這個類別會公開[IPropertyNotifySink](/windows/desktop/api/ocidl/nn-ocidl-ipropertynotifysink)作為可連接物件上的連出介面的介面。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template<class T, class CDV = CComDynamicUnkArray>
class IPropertyNotifySinkCP
   : public IConnectionPointImpl<T, &IID_IPropertyNotifySink, CDV>
```

#### <a name="parameters"></a>參數

*T*<br/>
您的類別，衍生自`IPropertyNotifySinkCP`。

*CDV*<br/>
類別可管理的連接點和其接收器之間的連線。 預設值是[CComDynamicUnkArray](../../atl/reference/ccomdynamicunkarray-class.md)，可讓連接無限制。 您也可以使用[CComUnkArray](../../atl/reference/ccomunkarray-class.md)，指定固定的連接數目。

## <a name="remarks"></a>備註

`IPropertyNotifySinkCP` 繼承其基底類別，透過的所有方法[IConnectionPointImpl](../../atl/reference/iconnectionpointimpl-class.md)。

[IPropertyNotifySink](/windows/desktop/api/ocidl/nn-ocidl-ipropertynotifysink)介面可讓接收物件，以接收有關屬性變更通知。 類別`IPropertyNotifySinkCP`會將此介面公開為可連接物件上的連出介面。 用戶端必須實作`IPropertyNotifySink`接收上的方法。

衍生您的類別，從`IPropertyNotifySinkCP`當您要建立連接點，表示`IPropertyNotifySink`介面。

如需有關如何使用 ATL 中的連接點的詳細資訊，請參閱[連接點](../../atl/atl-connection-points.md)。

## <a name="requirements"></a>需求

**標頭：** atlctl.h

## <a name="see-also"></a>另請參閱

[IConnectionPointImpl 類別](../../atl/reference/iconnectionpointimpl-class.md)<br/>
[IConnectionPointContainerImpl 類別](../../atl/reference/iconnectionpointcontainerimpl-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)
