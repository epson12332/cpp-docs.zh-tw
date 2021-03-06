---
title: CMFCImageEditorPaletteBar 類別
ms.date: 11/04/2016
f1_keywords:
- CMFCImageEditorPaletteBar
- AFXIMAGEEDITORDIALOG/CMFCImageEditorPaletteBar
- AFXIMAGEEDITORDIALOG/CMFCImageEditorPaletteBar::GetRowHeight
- AFXIMAGEEDITORDIALOG/CMFCImageEditorPaletteBar::IsButtonExtraSizeAvailable
helpviewer_keywords:
- CMFCImageEditorPaletteBar [MFC], GetRowHeight
- CMFCImageEditorPaletteBar [MFC], IsButtonExtraSizeAvailable
ms.assetid: 3fb7ba8e-f254-4d56-b913-9941b4ed8138
ms.openlocfilehash: 6812f3f425186484ef892d7f5c626c0dfce0f863
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62378098"
---
# <a name="cmfcimageeditorpalettebar-class"></a>CMFCImageEditorPaletteBar 類別

提供影像編輯器 對話方塊中的調色盤列功能。

## <a name="syntax"></a>語法

```
class CMFCImageEditorPaletteBar : public CMFCToolBar
```

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|||
|-|-|
|名稱|描述|
|[CMFCImageEditorPaletteBar::GetRowHeight](#getrowheight)|傳回的工具列按鈕的高度。 (覆寫[CMFCToolBar::GetRowHeight](../../mfc/reference/cmfctoolbar-class.md#getrowheight)。)|
|[CMFCImageEditorPaletteBar::IsButtonExtraSizeAvailable](#isbuttonextrasizeavailable)|判斷工具列是否可以顯示擴充框線的按鈕。 (覆寫[CMFCToolBar::IsButtonExtraSizeAvailable](../../mfc/reference/cmfctoolbar-class.md#isbuttonextrasizeavailable)。)|

### <a name="remarks"></a>備註

這個類別不是直接從您的程式碼使用。

架構會使用這個類別顯示調色盤列在 [影像編輯器] 對話方塊。 如需映像的 [編輯器] 對話方塊的詳細資訊，請參閱[CMFCImageEditorDialog 類別](../../mfc/reference/cmfcimageeditordialog-class.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CWnd](../../mfc/reference/cwnd-class.md)

[CBasePane](../../mfc/reference/cbasepane-class.md)

[CPane](../../mfc/reference/cpane-class.md)

[CMFCBaseToolBa](../../mfc/reference/cmfcbasetoolbar-class.md)

[CMFCToolBar](../../mfc/reference/cmfctoolbar-class.md)

[CMFCImageEditorPaletteBar](../../mfc/reference/cmfcimageeditorpalettebar-class.md)

## <a name="requirements"></a>需求

**標頭：** afximageeditordialog.h

##  <a name="getrowheight"></a>  CMFCImageEditorPaletteBar::GetRowHeight

傳回的工具列按鈕的高度。

```
virtual int GetRowHeight() const;
```

### <a name="return-value"></a>傳回值

在工具列上的每個按鈕的高度。

##  <a name="isbuttonextrasizeavailable"></a>  CMFCImageEditorPaletteBar::IsButtonExtraSizeAvailable

判斷工具列是否可以顯示擴充框線的按鈕。

```
virtual BOOL IsButtonExtraSizeAvailable() const;
```

### <a name="return-value"></a>傳回值

這個方法會傳回 FALSE。

## <a name="see-also"></a>另請參閱

[階層架構圖表](../../mfc/hierarchy-chart.md)<br/>
[類別](../../mfc/reference/mfc-classes.md)<br/>
[CMFCImageEditorDialog 類別](../../mfc/reference/cmfcimageeditordialog-class.md)
