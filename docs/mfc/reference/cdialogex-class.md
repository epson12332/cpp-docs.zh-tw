---
title: CDialogEx 類別
ms.date: 11/04/2016
f1_keywords:
- CDialogEx
- AFXDIALOGEX/CDialogEx
- AFXDIALOGEX/CDialogEx::CDialogEx
- AFXDIALOGEX/CDialogEx::SetBackgroundColor
- AFXDIALOGEX/CDialogEx::SetBackgroundImage
helpviewer_keywords:
- CDialogEx [MFC], CDialogEx
- CDialogEx [MFC], SetBackgroundColor
- CDialogEx [MFC], SetBackgroundImage
ms.assetid: a6ed3b1f-aef8-4b66-ac78-2160faf63c13
ms.openlocfilehash: f92058d1aa0dabccf6623d20a248fed8eb99ab26
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62168046"
---
# <a name="cdialogex-class"></a>CDialogEx 類別

`CDialogEx` 類別會指定對話方塊的背景影像和背景色彩。

## <a name="syntax"></a>語法

```
class CDialogEx : public CDialog
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CDialogEx::CDialogEx](#cdialogex)|建構 `CDialogEx` 物件。|
|`CDialogEx::~CDialogEx`|解構函式。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CDialogEx::SetBackgroundColor](#setbackgroundcolor)|設定對話方塊的背景色彩。|
|[CDialogEx::SetBackgroundImage](#setbackgroundimage)|設定對話方塊的背景影像。|

## <a name="remarks"></a>備註

若要使用 `CDialogEx` 類別，請將您的對話方塊類別從 `CDialogEx` 類別進行衍生，而不是從 `CDialog` 類別。

對話方塊影像會儲存在資源檔中。 架構會自動刪除從資源檔載入的任何影像。 若要以程式設計方式刪除目前的背景影像，請呼叫[CDialogEx::SetBackgroundImage](#setbackgroundimage)方法或實作`OnDestroy`事件處理常式。 當您呼叫[CDialogEx::SetBackgroundImage](#setbackgroundimage)方法，請傳入`HBITMAP`參數做為影像控點。 `CDialogEx` 物件會取得影像的擁有權，而若 `m_bAutoDestroyBmp` 旗標是 `TRUE` 的話，則會將它刪除。

A`CDialogEx`物件可以是父代[CMFCPopupMenu 類別](../../mfc/reference/cmfcpopupmenu-class.md)物件。 [CMFCPopupMenu 類別](../../mfc/reference/cmfcpopupmenu-class.md)物件會呼叫`CDialogEx::SetActiveMenu`方法時[CMFCPopupMenu 類別](../../mfc/reference/cmfcpopupmenu-class.md)物件開啟。 之後，`CDialogEx`物件會處理任何功能表事件，直到[CMFCPopupMenu 類別](../../mfc/reference/cmfcpopupmenu-class.md)物件已關閉。

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CWnd](../../mfc/reference/cwnd-class.md)

[CDialog](../../mfc/reference/cdialog-class.md)

[CDialogEx](../../mfc/reference/cdialogex-class.md)

## <a name="requirements"></a>需求

**標頭：** afxdialogex.h

##  <a name="cdialogex"></a>  CDialogEx::CDialogEx

建構 `CDialogEx` 物件。

```
CDialogEx(
    UINT nIDTemplate,
    CWnd* pParent=NULL);

CDialogEx(
    LPCTSTR lpszTemplateName,
    CWnd* pParentWnd=NULL);
```

### <a name="parameters"></a>參數

*nIDTemplate*<br/>
[in]對話方塊範本資源識別碼。

*lpszTemplateName*<br/>
[in]對話方塊範本資源名稱。

*pParent*<br/>
[in]父視窗的指標。 預設值是 NULL。

*pParentWnd*<br/>
[in]父視窗的指標。 預設值是 NULL。

### <a name="return-value"></a>傳回值

### <a name="remarks"></a>備註

##  <a name="setbackgroundcolor"></a>  CDialogEx::SetBackgroundColor

設定對話方塊的背景色彩。

```
void SetBackgroundColor(
    COLORREF color,
    BOOL bRepaint=TRUE);
```

### <a name="parameters"></a>參數

*color*<br/>
[in]RGB 色彩值。

*bRepaint*<br/>
[in]若要立即更新畫面; TRUE否則為 FALSE。 預設值為 TRUE。

### <a name="remarks"></a>備註

##  <a name="setbackgroundimage"></a>  CDialogEx::SetBackgroundImage

設定對話方塊的背景影像。

```
void SetBackgroundImage(
    HBITMAP hBitmap,
    BackgroundLocation location=BACKGR_TILE,
    BOOL bAutoDestroy=TRUE,
    BOOL bRepaint=TRUE);

BOOL SetBackgroundImage(
    UINT uiBmpResId,
    BackgroundLocation location=BACKGR_TILE,
    BOOL bRepaint=TRUE);
```

### <a name="parameters"></a>參數

*hBitmap*<br/>
[in]背景影像控制代碼。

*uiBmpResId*<br/>
[in]背景影像的資源識別碼。

*location*<br/>
[in]其中一個`CDialogEx::BackgroundLocation`指定映像的位置的值。 有效值包括 BACKGR_TILE、 BACKGR_TOPLEFT、 BACKGR_TOPRIGHT、 BACKGR_BOTTOMLEFT 和 BACKGR_BOTTOMRIGHT。 預設值是 BACKGR_TILE。

*bAutoDestroy*<br/>
[in]為 true，則會自動終結背景影像否則為 FALSE。

*bRepaint*<br/>
[in]若要立即重繪對話方塊中，TRUE否則為 FALSE。

### <a name="return-value"></a>傳回值

在第二個方法多載的語法，為 true，則如果方法成功，否則為 FALSE。

### <a name="remarks"></a>備註

您所指定的映像不會自動縮放以符合對話方塊用戶端區域。

## <a name="see-also"></a>另請參閱

[階層架構圖表](../../mfc/hierarchy-chart.md)<br/>
[類別](../../mfc/reference/mfc-classes.md)<br/>
[CMFCPopupMenu 類別](../../mfc/reference/cmfcpopupmenu-class.md)<br/>
[CContextMenuManager 類別](../../mfc/reference/ccontextmenumanager-class.md)
