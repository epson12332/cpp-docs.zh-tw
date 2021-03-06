---
title: CMFCToolTipCtrl 類別
ms.date: 11/04/2016
f1_keywords:
- CMFCToolTipCtrl
- AFXTOOLTIPCTRL/CMFCToolTipCtrl
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::GetIconSize
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::GetParams
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnDrawBorder
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnDrawDescription
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnDrawIcon
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnDrawLabel
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnDrawSeparator
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::OnFillBackground
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::SetDescription
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::SetFixedWidth
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::SetHotRibbonButton
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::SetLocation
- AFXTOOLTIPCTRL/CMFCToolTipCtrl::SetParams
helpviewer_keywords:
- CMFCToolTipCtrl [MFC], GetIconSize
- CMFCToolTipCtrl [MFC], GetParams
- CMFCToolTipCtrl [MFC], OnDrawBorder
- CMFCToolTipCtrl [MFC], OnDrawDescription
- CMFCToolTipCtrl [MFC], OnDrawIcon
- CMFCToolTipCtrl [MFC], OnDrawLabel
- CMFCToolTipCtrl [MFC], OnDrawSeparator
- CMFCToolTipCtrl [MFC], OnFillBackground
- CMFCToolTipCtrl [MFC], SetDescription
- CMFCToolTipCtrl [MFC], SetFixedWidth
- CMFCToolTipCtrl [MFC], SetHotRibbonButton
- CMFCToolTipCtrl [MFC], SetLocation
- CMFCToolTipCtrl [MFC], SetParams
ms.assetid: 9fbfcfb1-a8ab-417f-ae29-9a9ca85ee58f
ms.openlocfilehash: aaf9d9570906b7886d8ec78575c39db5d62099f7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62388302"
---
# <a name="cmfctooltipctrl-class"></a>CMFCToolTipCtrl 類別

根據 [CToolTipCtrl Class](../../mfc/reference/ctooltipctrl-class.md)的擴充工具提示實作。 根據 `CMFCToolTipCtrl` 類別的工具提示可以顯示圖示、標籤和描述。 您可以使用漸層填滿、自訂文字和框線色彩、粗體文字、圓角或氣球樣式，自訂其視覺外觀。

如需詳細資訊，請參閱中的原始程式碼**VC\\atlmfc\\src\\mfc** Visual Studio 安裝資料夾。

## <a name="syntax"></a>語法

```
class CMFCToolTipCtrl : public CToolTipCtrl
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|`CMFCToolTipCtrl::CMFCToolTipCtrl`|預設建構函式。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CMFCToolTipCtrl::GetIconSize](#geticonsize)|傳回工具提示中的圖示大小。|
|[CMFCToolTipCtrl::GetParams](#getparams)|傳回工具提示的顯示設定。|
|[CMFCToolTipCtrl::OnDrawBorder](#ondrawborder)|繪製工具提示的框線。|
|[CMFCToolTipCtrl::OnDrawDescription](#ondrawdescription)||
|[CMFCToolTipCtrl::OnDrawIcon](#ondrawicon)|在工具提示中顯示圖示。|
|[CMFCToolTipCtrl::OnDrawLabel](#ondrawlabel)|繪製工具提示的標籤，或計算標籤的大小。|
|[CMFCToolTipCtrl::OnDrawSeparator](#ondrawseparator)|工具提示中的標籤和描述之間繪製分隔符號。|
|[CMFCToolTipCtrl::OnFillBackground](#onfillbackground)|填滿工具提示背景。|
|[CMFCToolTipCtrl::SetDescription](#setdescription)|設定要由工具提示顯示的描述。|
|[CMFCToolTipCtrl::SetFixedWidth](#setfixedwidth)||
|[CMFCToolTipCtrl::SetHotRibbonButton](#sethotribbonbutton)||
|[CMFCToolTipCtrl::SetLocation](#setlocation)||
|[CMFCToolTipCtrl::SetParams](#setparams)|使用 `CMFCToolTipInfo` 物件指定工具提示的視覺外觀。|

## <a name="remarks"></a>備註

使用`CMFCToolTipCtrl`， `CMFCToolTipInfo`，並[CTooltipManager 類別](../../mfc/reference/ctooltipmanager-class.md)應用程式中實作自訂的工具提示的物件。

例如，若要使用氣球樣式工具提示，請依照下列步驟：

1. 使用[CWinAppEx 類別](../../mfc/reference/cwinappex-class.md)方法以初始化應用程式中的工具提示管理員。

2. 建立 `CMFCToolTipInfo` 結構來指定您想要的視覺樣式：

```
CMFCToolTipInfo params;
    params.m_bBoldLabel = FALSE;
    params.m_bDrawDescription = FALSE;
    params.m_bDrawIcon = FALSE;
    params.m_bRoundedCorners = TRUE;
    params.m_bDrawSeparator = FALSE;
    if (m_bCustomColors)
{
    params.m_clrFill = RGB (255,
    255,
    255);

    params.m_clrFillGradient = RGB (228,
    228,
    240);

    params.m_clrText = RGB (61,
    83,
    80);

    params.m_clrBorder = RGB (144,
    149,
    168);

}
```
3. 使用[Settooltipparams](../../mfc/reference/ctooltipmanager-class.md#settooltipparams)方法，將所有的工具提示的視覺樣式應用程式中設定使用中定義的樣式`CMFCToolTipInfo`物件：

```
theApp.GetTooltipManager ()->SetTooltipParams (AFX_TOOLTIP_TYPE_ALL,
    RUNTIME_CLASS (CMFCToolTipCtrl), &params);
```
您也可以從 `CMFCToolTipCtrl` 衍生新的類別，以控制工具提示的行為和呈現。 若要指定新的工具提示控制項類別，請使用 `CTooltipManager::SetTooltipParams` 方法：

```
myApp.GetTooltipManager ()->SetTooltipParams (AFX_TOOLTIP_TYPE_ALL,
    RUNTIME_CLASS (CMyToolTipCtrl))
```
若要還原預設工具提示控制類別，並將工具提示外觀重設為預設狀態，請在 `SetTooltipParams` 的執行階段類別和工具提示資訊參數中指定 NULL：

```
theApp.GetTooltipManager ()->SetTooltipParams (AFX_TOOLTIP_TYPE_ALL,
    NULL,
    NULL);
```

## <a name="example"></a>範例

下列範例示範如何建構 `CMFCToolTipCtrl` 物件、設定工具提示顯示的描述，以及設定工具提示控制項的寬度。

[!code-cpp[NVC_MFC_RibbonApp#41](../../mfc/reference/codesnippet/cpp/cmfctooltipctrl-class_1.cpp)]

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CWnd](../../mfc/reference/cwnd-class.md)

[CToolTipCtrl](../../mfc/reference/ctooltipctrl-class.md)

[CMFCToolTipCtrl](../../mfc/reference/cmfctooltipctrl-class.md)

## <a name="requirements"></a>需求

**標頭：** afxtooltipctrl.h

##  <a name="cmfctooltipctrl"></a>  CMFCToolTipCtrl::CMFCToolTipCtrl

```
CMFCToolTipCtrl(CMFCToolTipInfo* pParams = NULL);
```

### <a name="parameters"></a>參數

[in] *pParams*<br/>

### <a name="remarks"></a>備註

##  <a name="geticonsize"></a>  CMFCToolTipCtrl::GetIconSize

傳回工具提示中的圖示大小。

```
virtual CSize GetIconSize();
```

### <a name="return-value"></a>傳回值

圖示，像素為單位的大小。

##  <a name="getparams"></a>  CMFCToolTipCtrl::GetParams

傳回工具提示的顯示設定。

```
const CMFCToolTipInfo& GetParams() const;
```

### <a name="return-value"></a>傳回值

目前的工具提示顯示設定，會儲存在[CMFCToolTipInfo 類別](../../mfc/reference/cmfctooltipinfo-class.md)物件。

##  <a name="ondrawborder"></a>  CMFCToolTipCtrl::OnDrawBorder

繪製工具提示的框線。

```
virtual void OnDrawBorder(
    CDC* pDC,
    CRect rect,
    COLORREF clrLine);
```

### <a name="parameters"></a>參數

*pDC*<br/>
[in]裝置內容指標。

*rect*<br/>
[in]工具提示的週框。

*clrLine*<br/>
[in]框線色彩。

### <a name="remarks"></a>備註

覆寫這個方法在衍生類別來自訂工具提示框線外觀。

##  <a name="ondrawdescription"></a>  CMFCToolTipCtrl::OnDrawDescription

```
virtual CSize OnDrawDescription(
    CDC* pDC,
    CRect rect,
    BOOL bCalcOnly);
```

### <a name="parameters"></a>參數

[in] *pDC*<br/>
[in] *rect*<br/>
[in] *bCalcOnly*<br/>

### <a name="return-value"></a>傳回值

### <a name="remarks"></a>備註

##  <a name="ondrawicon"></a>  CMFCToolTipCtrl::OnDrawIcon

在工具提示中顯示圖示。

```
virtual BOOL OnDrawIcon(
    CDC* pDC,
    CRect rectImage);
```

### <a name="parameters"></a>參數

*pDC*<br/>
[in]裝置內容指標。

*rectImage*<br/>
[in]圖示的座標。

### <a name="return-value"></a>傳回值

所繪製的圖示，其值為 TRUE。 否則為 FALSE。

### <a name="remarks"></a>備註

覆寫此方法在衍生的類別，以顯示自訂圖示。 您也必須覆寫[CMFCToolTipCtrl::GetIconSize](#geticonsize)若要啟用以正確計算文字與描述的版面配置的工具提示。

##  <a name="ondrawlabel"></a>  CMFCToolTipCtrl::OnDrawLabel

繪製工具提示的標籤，或計算標籤的大小。

```
virtual CSize OnDrawLabel(
    CDC* pDC,
    CRect rect,
    BOOL bCalcOnly);
```

### <a name="parameters"></a>參數

*pDC*<br/>
[in]裝置內容指標。

*rect*<br/>
[in][標籤] 區域的周框。

*bCalcOnly*<br/>
[in]如果為 TRUE，就不會繪製標籤。

### <a name="return-value"></a>傳回值

標籤，像素為單位的大小。

### <a name="remarks"></a>備註

如果您想要自訂的工具提示標籤外觀，請覆寫這個方法在衍生類別中。

##  <a name="ondrawseparator"></a>  CMFCToolTipCtrl::OnDrawSeparator

工具提示中的標籤和描述之間繪製分隔符號。

```
virtual void OnDrawSeparator(
    CDC* pDC,
    int x1,
    int x2,
    int y);
```

### <a name="parameters"></a>參數

*pDC*<br/>
[in]裝置內容指標。

*x1*<br/>
[in]水平分隔符號的左邊座標。

*x2*<br/>
[in]水平分隔符號的右邊座標。

*Y*<br/>
[in]分隔線的垂直座標。

### <a name="remarks"></a>備註

預設實作會繪製一條線從點 (x1，y) 到點 (x2，y)。

覆寫這個方法來自訂外觀，分隔符號的衍生類別中。

##  <a name="onfillbackground"></a>  CMFCToolTipCtrl::OnFillBackground

填滿工具提示背景。

```
virtual void OnFillBackground(
    CDC* pDC,
    CRect rect,
    COLORREF& clrText,
    COLORREF& clrLine);
```

### <a name="parameters"></a>參數

*pDC*<br/>
[in]裝置內容指標。

*rect*<br/>
[in]指定要填滿區域的週框矩形。

*clrText*<br/>
[in]工具提示的前景色彩。

*clrLine*<br/>
[in]色彩的框線和分隔符號之間的線條標籤和描述。

### <a name="remarks"></a>備註

預設實作會填滿所指定的矩形*rect*使用的色彩或最新的呼叫所指定的圖樣[CMFCToolTipCtrl::SetParams](#setparams)。

如果您想要自訂的工具提示外觀，請覆寫這個方法在衍生類別中。

##  <a name="setdescription"></a>  CMFCToolTipCtrl::SetDescription

設定要由工具提示顯示的描述。

```
virtual void SetDescription(const CString strDesrciption);
```

### <a name="parameters"></a>參數

*strDesrciption*<br/>
[in]描述文字。

### <a name="remarks"></a>備註

描述文字會顯示在工具提示下分隔符號。

##  <a name="setfixedwidth"></a>  CMFCToolTipCtrl::SetFixedWidth

```
void SetFixedWidth(
    int nWidthRegular,
    int nWidthLargeImage);
```

### <a name="parameters"></a>參數

[in] *nWidthRegular*<br/>
[in] *nWidthLargeImage*<br/>

### <a name="remarks"></a>備註

##  <a name="sethotribbonbutton"></a>  CMFCToolTipCtrl::SetHotRibbonButton

```
void SetHotRibbonButton(CMFCRibbonButton* pRibbonButton);
```

### <a name="parameters"></a>參數

[in] *pRibbonButton*<br/>

### <a name="remarks"></a>備註

##  <a name="setlocation"></a>  CMFCToolTipCtrl::SetLocation

```
void SetLocation(CPoint pt);
```

### <a name="parameters"></a>參數

[in] *pt*<br/>

### <a name="remarks"></a>備註

##  <a name="setparams"></a>  CMFCToolTipCtrl::SetParams

使用指定的工具提示的視覺外觀[CMFCToolTipInfo 類別](../../mfc/reference/cmfctooltipinfo-class.md)物件。

```
void SetParams(CMFCToolTipInfo* pParams);
```

### <a name="parameters"></a>參數

*pParams*<br/>
[in]指標[CMFCToolTipInfo 類別](../../mfc/reference/cmfctooltipinfo-class.md)物件，包含顯示參數。

### <a name="remarks"></a>備註

會顯示工具提示，使用色彩來繪製視覺化樣式，每當*pParams*指定。 值*pParams*會儲存在受保護的成員`m_Params`，存取由衍生類別覆寫[CMFCToolTipCtrl::OnDrawBorder](#ondrawborder)， [CMFCToolTipCtrl:: OnDrawIcon](#ondrawicon)， [CMFCToolTipCtrl::OnDrawLabel](#ondrawlabel)， [CMFCToolTipCtrl::OnDrawSeparator](#ondrawseparator)，或[CMFCToolTipCtrl::OnFillBackground](#onfillbackground)維護指定的外觀。

## <a name="see-also"></a>另請參閱

[階層架構圖表](../../mfc/hierarchy-chart.md)<br/>
[類別](../../mfc/reference/mfc-classes.md)<br/>
[CToolTipCtrl 類別](../../mfc/reference/ctooltipctrl-class.md)<br/>
[CTooltipManager 類別](../../mfc/reference/ctooltipmanager-class.md)<br/>
[CMFCToolTipInfo 類別](../../mfc/reference/cmfctooltipinfo-class.md)<br/>
[CWinAppEx 類別](../../mfc/reference/cwinappex-class.md)
