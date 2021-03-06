---
title: CComControl 類別
ms.date: 11/04/2016
f1_keywords:
- CComControl
- ATLCTL/ATL::CComControl
- ATLCTL/ATL::CComControl::CComControl
- ATLCTL/ATL::CComControl::ControlQueryInterface
- ATLCTL/ATL::CComControl::CreateControlWindow
- ATLCTL/ATL::CComControl::FireOnChanged
- ATLCTL/ATL::CComControl::FireOnRequestEdit
- ATLCTL/ATL::CComControl::MessageBox
helpviewer_keywords:
- control flags
- CComControlBase class, CComControl class
- stock properties, ATL
- CComControl class
- controls [ATL], control helper functions
- ambient properties
- controls [ATL], properties
ms.assetid: 55368c27-bd16-45a7-b701-edb36157c8e8
ms.openlocfilehash: ffbec7c1a83c0dd829878f4c73340528d32fb852
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62246495"
---
# <a name="ccomcontrol-class"></a>CComControl 類別

這個類別提供方法來建立及管理 ATL 的控制項。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template <class T, class WinBase = CWindowImpl<T>>
class ATL_NO_VTABLE CComControl : public CComControlBase,
    public WinBase;
```

#### <a name="parameters"></a>參數

*T*<br/>
實作控制項的類別。

*WinBase*<br/>
實作視窗化函式的基底類別。 預設值為[CWindowImpl](../../atl/reference/cwindowimpl-class.md)。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CComControl::CComControl](#ccomcontrol)|建構函式。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CComControl::ControlQueryInterface](#controlqueryinterface)|擷取所要求介面的指標。|
|[CComControl::CreateControlWindow](#createcontrolwindow)|建立控制項的視窗。|
|[CComControl::FireOnChanged](#fireonchanged)|通知容器接收已變更的控制項屬性。|
|[CComControl::FireOnRequestEdit](#fireonrequestedit)|控制項屬性即將變更，而且物件會要求接收器要如何繼續進行，請通知容器的接收。|
|[CComControl::MessageBox](#messagebox)|呼叫這個方法來建立、 顯示和操作訊息方塊。|

## <a name="remarks"></a>備註

`CComControl` 是一組實用的控制項 helper 函式和 ATL 的控制項的基本資料成員。 當您建立標準控制項或 DHTML 控制項使用 ATL 控制項精靈時，精靈會自動衍生您的類別，從`CComControl`。 `CComControl` 衍生大部分的方法從[CComControlBase](../../atl/reference/ccomcontrolbase-class.md)。

如需建立控制項的詳細資訊，請參閱[ATL 教學課程](../../atl/active-template-library-atl-tutorial.md)。 如需 ATL 專案精靈 的詳細資訊，請參閱文章[建立 ATL 專案](../../atl/reference/creating-an-atl-project.md)。

如需示範`CComControl`方法和資料成員，請參閱[CIRC](../../overview/visual-cpp-samples.md)範例。

## <a name="inheritance-hierarchy"></a>繼承階層

`WinBase`

[CComControlBase](../../atl/reference/ccomcontrolbase-class.md)

`CComControl`

## <a name="requirements"></a>需求

**標頭：** atlctl.h

##  <a name="ccomcontrol"></a>  CComControl::CComControl

建構函式。

```
CComControl();
```

### <a name="remarks"></a>備註

呼叫[CComControlBase](ccomcontrolbase-class.md#ccomcontrolbase)建構函式，傳遞`m_hWnd`透過繼承的資料成員[CWindowImpl](../../atl/reference/cwindowimpl-class.md)。

##  <a name="controlqueryinterface"></a>  CComControl::ControlQueryInterface

擷取所要求介面的指標。

```
virtual HRESULT ControlQueryInterface(const IID& iid, void** ppv);
```

### <a name="parameters"></a>參數

*iid*<br/>
[in]所要求介面的 GUID。

*ppv*<br/>
[out]所識別之介面指標的指標*iid*，或如果找不到介面則為 NULL。

### <a name="remarks"></a>備註

只會處理 COM 對應表格中的介面。

### <a name="example"></a>範例

[!code-cpp[NVC_ATL_COM#15](../../atl/codesnippet/cpp/ccomcontrol-class_1.cpp)]

##  <a name="createcontrolwindow"></a>  CComControl::CreateControlWindow

根據預設，建立控制項的視窗呼叫`CWindowImpl::Create`。

```
virtual HWND CreateControlWindow(HWND hWndParent, RECT& rcPos);
```

### <a name="parameters"></a>參數

*hWndParent*<br/>
[in]父系或擁有者的視窗控制代碼。 必須提供有效的視窗控制代碼。 [控制] 視窗會侷限於其父視窗的區域。

*rcPos*<br/>
[in]初始大小和位置來建立視窗。

### <a name="remarks"></a>備註

如果您想要執行一些動作，請覆寫此方法以外建立的單一視窗，比方說，若要建立兩個視窗，其中會變成工具列控制項。

### <a name="example"></a>範例

[!code-cpp[NVC_ATL_COM#16](../../atl/codesnippet/cpp/ccomcontrol-class_2.cpp)]

##  <a name="fireonchanged"></a>  CComControl::FireOnChanged

通知容器接收已變更的控制項屬性。

```
HRESULT FireOnChanged(DISPID dispID);
```

### <a name="parameters"></a>參數

*dispID*<br/>
[in]已變更之屬性的識別項。

### <a name="return-value"></a>傳回值

其中一個標準的 HRESULT 值。

### <a name="remarks"></a>備註

如果您的控制項類別衍生自[IPropertyNotifySink](/windows/desktop/api/ocidl/nn-ocidl-ipropertynotifysink)，這個方法會呼叫[CFirePropNotifyEvent::FireOnChanged](cfirepropnotifyevent-class.md#fireonchanged)通知所有連線`IPropertyNotifySink`介面指定的控制項屬性已變更。 如果您的控制項類別未衍生自`IPropertyNotifySink`，這個方法會傳回 S_OK。

這個方法可以安全地呼叫，即使您的控制項不支援連接點。

### <a name="example"></a>範例

[!code-cpp[NVC_ATL_COM#17](../../atl/codesnippet/cpp/ccomcontrol-class_3.cpp)]

##  <a name="fireonrequestedit"></a>  CComControl::FireOnRequestEdit

控制項屬性即將變更，而且物件會要求接收器要如何繼續進行，請通知容器的接收。

```
HRESULT FireOnRequestEdit(DISPID dispID);
```

### <a name="parameters"></a>參數

*dispID*<br/>
[in]若要變更之屬性的識別項。

### <a name="return-value"></a>傳回值

其中一個標準的 HRESULT 值。

### <a name="remarks"></a>備註

如果您的控制項類別衍生自[IPropertyNotifySink](/windows/desktop/api/ocidl/nn-ocidl-ipropertynotifysink)，這個方法會呼叫[CFirePropNotifyEvent::FireOnRequestEdit](cfirepropnotifyevent-class.md#fireonrequestedit)通知所有連線`IPropertyNotifySink`介面指定控制項屬性即將變更。 如果您的控制項類別未衍生自`IPropertyNotifySink`，這個方法會傳回 S_OK。

這個方法可以安全地呼叫，即使您的控制項不支援連接點。

### <a name="example"></a>範例

[!code-cpp[NVC_ATL_COM#18](../../atl/codesnippet/cpp/ccomcontrol-class_4.cpp)]

##  <a name="messagebox"></a>  CComControl::MessageBox

呼叫這個方法來建立、 顯示和操作訊息方塊。

```
int MessageBox(
    LPCTSTR lpszText,
    LPCTSTR lpszCaption = _T(""),
    UINT nType = MB_OK);
```

### <a name="parameters"></a>參數

*lpszText*<br/>
要在訊息方塊中顯示的文字。

*lpszCaption*<br/>
對話方塊的標題。 如果 NULL （預設值），在使用 「 錯誤 」 的標題。

*nType*<br/>
指定的內容和對話方塊的行為。 請參閱[MessageBox](/windows/desktop/api/winuser/nf-winuser-messagebox)清單的 Windows SDK 文件可用的不同的訊息方塊中的項目。 預設提供的簡單**確定** 按鈕。

### <a name="return-value"></a>傳回值

傳回整數值，指定之下所列的功能表項目值的其中一個[MessageBox](/windows/desktop/api/winuser/nf-winuser-messagebox) Windows SDK 文件。

### <a name="remarks"></a>備註

`MessageBox` 同時在開發期間，以及輕鬆地向使用者顯示錯誤或警告訊息，則會很有用。

## <a name="see-also"></a>另請參閱

[CWindowImpl 類別](../../atl/reference/cwindowimpl-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)<br/>
[CComControlBase 類別](../../atl/reference/ccomcontrolbase-class.md)<br/>
[CComCompositeControl 類別](../../atl/reference/ccomcompositecontrol-class.md)
