---
title: "CTabCtrl 類別 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- CTabCtrl
- AFXCMN/CTabCtrl
- AFXCMN/CTabCtrl::CTabCtrl
- AFXCMN/CTabCtrl::AdjustRect
- AFXCMN/CTabCtrl::Create
- AFXCMN/CTabCtrl::CreateEx
- AFXCMN/CTabCtrl::DeleteAllItems
- AFXCMN/CTabCtrl::DeleteItem
- AFXCMN/CTabCtrl::DeselectAll
- AFXCMN/CTabCtrl::DrawItem
- AFXCMN/CTabCtrl::GetCurFocus
- AFXCMN/CTabCtrl::GetCurSel
- AFXCMN/CTabCtrl::GetExtendedStyle
- AFXCMN/CTabCtrl::GetImageList
- AFXCMN/CTabCtrl::GetItem
- AFXCMN/CTabCtrl::GetItemCount
- AFXCMN/CTabCtrl::GetItemRect
- AFXCMN/CTabCtrl::GetItemState
- AFXCMN/CTabCtrl::GetRowCount
- AFXCMN/CTabCtrl::GetToolTips
- AFXCMN/CTabCtrl::HighlightItem
- AFXCMN/CTabCtrl::HitTest
- AFXCMN/CTabCtrl::InsertItem
- AFXCMN/CTabCtrl::RemoveImage
- AFXCMN/CTabCtrl::SetCurFocus
- AFXCMN/CTabCtrl::SetCurSel
- AFXCMN/CTabCtrl::SetExtendedStyle
- AFXCMN/CTabCtrl::SetImageList
- AFXCMN/CTabCtrl::SetItem
- AFXCMN/CTabCtrl::SetItemExtra
- AFXCMN/CTabCtrl::SetItemSize
- AFXCMN/CTabCtrl::SetItemState
- AFXCMN/CTabCtrl::SetMinTabWidth
- AFXCMN/CTabCtrl::SetPadding
- AFXCMN/CTabCtrl::SetToolTips
dev_langs: C++
helpviewer_keywords:
- CTabCtrl [MFC], CTabCtrl
- CTabCtrl [MFC], AdjustRect
- CTabCtrl [MFC], Create
- CTabCtrl [MFC], CreateEx
- CTabCtrl [MFC], DeleteAllItems
- CTabCtrl [MFC], DeleteItem
- CTabCtrl [MFC], DeselectAll
- CTabCtrl [MFC], DrawItem
- CTabCtrl [MFC], GetCurFocus
- CTabCtrl [MFC], GetCurSel
- CTabCtrl [MFC], GetExtendedStyle
- CTabCtrl [MFC], GetImageList
- CTabCtrl [MFC], GetItem
- CTabCtrl [MFC], GetItemCount
- CTabCtrl [MFC], GetItemRect
- CTabCtrl [MFC], GetItemState
- CTabCtrl [MFC], GetRowCount
- CTabCtrl [MFC], GetToolTips
- CTabCtrl [MFC], HighlightItem
- CTabCtrl [MFC], HitTest
- CTabCtrl [MFC], InsertItem
- CTabCtrl [MFC], RemoveImage
- CTabCtrl [MFC], SetCurFocus
- CTabCtrl [MFC], SetCurSel
- CTabCtrl [MFC], SetExtendedStyle
- CTabCtrl [MFC], SetImageList
- CTabCtrl [MFC], SetItem
- CTabCtrl [MFC], SetItemExtra
- CTabCtrl [MFC], SetItemSize
- CTabCtrl [MFC], SetItemState
- CTabCtrl [MFC], SetMinTabWidth
- CTabCtrl [MFC], SetPadding
- CTabCtrl [MFC], SetToolTips
ms.assetid: 42e4aff6-46ae-4b2c-beaa-d1dce8d82138
caps.latest.revision: "21"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.workload: cplusplus
ms.openlocfilehash: ed981a2f7345a59f3df479bcd82b9326fd84de12
ms.sourcegitcommit: 8fa8fdf0fbb4f57950f1e8f4f9b81b4d39ec7d7a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="ctabctrl-class"></a>CTabCtrl 類別
提供 Windows 通用索引標籤控制項的功能。  
  
## <a name="syntax"></a>語法  
  
```  
class CTabCtrl : public CWnd  
```  
  
## <a name="members"></a>成員  
  
### <a name="public-constructors"></a>公用建構函式  
  
|名稱|描述|  
|----------|-----------------|  
|[CTabCtrl::CTabCtrl](#ctabctrl)|建構 `CTabCtrl` 物件。|  
  
### <a name="public-methods"></a>公用方法  
  
|名稱|描述|  
|----------|-----------------|  
|[CTabCtrl::AdjustRect](#adjustrect)|計算索引標籤控制項的顯示區域提供視窗矩形中，或計算視窗矩形，就會對應至指定的顯示區域。|  
|[CTabCtrl::Create](#create)|建立索引標籤控制項，並將其附加至執行個體的`CTabCtrl`物件。|  
|[CTabCtrl::CreateEx](#createex)|建立具有指定的 Windows 延伸樣式 索引標籤控制項，並將其附加至執行個體的`CTabCtrl`物件。|  
|[CTabCtrl::DeleteAllItems](#deleteallitems)|移除索引標籤控制項中的所有項目。|  
|[CTabCtrl::DeleteItem](#deleteitem)|移除索引標籤控制項中的項目。|  
|[CTabCtrl::DeselectAll](#deselectall)|重設在索引標籤控制項中，清除已按下的任何項目。|  
|[CTabCtrl::DrawItem](#drawitem)|繪製指定的項目索引標籤控制項。|  
|[CTabCtrl::GetCurFocus](#getcurfocus)|擷取具有目前焦點所在的索引標籤控制項的索引標籤。|  
|[CTabCtrl::GetCurSel](#getcursel)|決定索引標籤控制項中目前選取的索引標籤。|  
|[CTabCtrl::GetExtendedStyle](#getextendedstyle)|擷取目前正在使用的索引標籤控制項中的延伸的樣式。|  
|[CTabCtrl::GetImageList](#getimagelist)|擷取影像清單索引標籤控制項相關聯。|  
|[CTabCtrl::GetItem](#getitem)|擷取索引標籤控制項中的索引標籤的相關資訊。|  
|[CTabCtrl::GetItemCount](#getitemcount)|擷取索引標籤控制項中的索引標籤數目。|  
|[CTabCtrl::GetItemRect](#getitemrect)|擷取索引標籤控制項中的索引標籤的週框矩形。|  
|[CTabCtrl::GetItemState](#getitemstate)|擷取指定的索引標籤控制項項目的狀態。|  
|[CTabCtrl::GetRowCount](#getrowcount)|擷取目前的索引標籤控制項中的索引標籤的資料列數。|  
|[CTabCtrl::GetToolTips](#gettooltips)|擷取索引標籤控制項相關聯的工具提示控制項的控制代碼。|  
|[CTabCtrl::HighlightItem](#highlightitem)|設定反白顯示的狀態索引標籤項目。|  
|[CTabCtrl::HitTest](#hittest)|判斷哪些索引標籤上，如果有的話，是在指定的螢幕位置。|  
|[Ctabctrl:: Insertitem](#insertitem)|索引標籤控制項中插入新的索引標籤。|  
|[CTabCtrl::RemoveImage](#removeimage)|索引標籤控制項影像清單中移除映像。|  
|[CTabCtrl::SetCurFocus](#setcurfocus)|將焦點設定到索引標籤控制項中指定之索引標籤。|  
|[CTabCtrl::SetCurSel](#setcursel)|索引標籤控制項中選取索引標籤。|  
|[CTabCtrl::SetExtendedStyle](#setextendedstyle)|設定索引標籤控制項的延伸的樣式。|  
|[CTabCtrl::SetImageList](#setimagelist)|指定索引標籤控制項影像清單。|  
|[CTabCtrl::SetItem](#setitem)|設定下列部分或所有索引標籤的屬性。|  
|[CTabCtrl::SetItemExtra](#setitemextra)|設定每個索引標籤的索引標籤控制項中的應用程式定義的資料保留的位元組數目。|  
|[CTabCtrl::SetItemSize](#setitemsize)|設定項目的高度與寬度。|  
|[CTabCtrl::SetItemState](#setitemstate)|將指定的索引標籤控制項項目狀態設定。|  
|[CTabCtrl::SetMinTabWidth](#setmintabwidth)|索引標籤控制項中設定的最小寬度的項目。|  
|[CTabCtrl::SetPadding](#setpadding)|設定 （填補） 每個索引標籤的圖示和標籤控制項中的標籤周圍的空間數量。|  
|[CTabCtrl::SetToolTips](#settooltips)|將工具提示控制項指派給索引標籤控制項。|  
  
## <a name="remarks"></a>備註  
 「 索引標籤控制項 」 是類似於筆記本中的分隔線或檔案櫃中的標籤。 藉由使用索引標籤控制項，應用程式可以定義視窗或對話方塊中同一個區域的多個頁面。 每個頁面所組成的一組資訊或一群應用程式會顯示當使用者選取 [對應] 索引標籤的控制項。一種特殊的索引標籤控制項顯示看起來像按鈕的索引標籤。 按一下按鈕應該立即執行命令，而不要顯示的頁面。  
  
 這個控制項 (因此`CTabCtrl`類別) 僅適用於 Windows 95/98、 Windows NT 的版本 3.51 下執行的程式和更新版本。  
  
 如需有關使用`CTabCtrl`，請參閱[控制項](../../mfc/controls-mfc.md)和[使用 CTabCtrl](../../mfc/using-ctabctrl.md)。  
  
## <a name="inheritance-hierarchy"></a>繼承階層  
 [CObject](../../mfc/reference/cobject-class.md)  
  
 [CCmdTarget](../../mfc/reference/ccmdtarget-class.md)  
  
 [CWnd](../../mfc/reference/cwnd-class.md)  
  
 `CTabCtrl`  
  
## <a name="requirements"></a>需求  
 **標頭：** afxcmn.h  
  
##  <a name="adjustrect"></a>CTabCtrl::AdjustRect  
 計算索引標籤控制項的顯示區域提供視窗矩形中，或計算視窗矩形，就會對應至指定的顯示區域。  
  
```  
void AdjustRect(BOOL bLarger,   LPRECT lpRect);
```  
  
### <a name="parameters"></a>參數  
 `bLarger`  
 表示要執行哪些作業。 如果這個參數是**TRUE**，`lpRect`指定顯示矩形，並接收對應視窗矩形。 如果這個參數是**FALSE**，`lpRect`指定視窗矩形，並接收對應的顯示矩形。  
  
 `lpRect`  
 指標[RECT](http://msdn.microsoft.com/library/windows/desktop/dd162897)結構，以指定給定的矩形，並接收計算出的矩形。  
  
### <a name="example"></a>範例  
 [!code-cpp[NVC_MFC_CTabCtrl#1](../../mfc/reference/codesnippet/cpp/ctabctrl-class_1.cpp)]  
  
##  <a name="create"></a>CTabCtrl::Create  
 建立索引標籤控制項，並將其附加至執行個體的`CTabCtrl`物件。  
  
```  
virtual BOOL Create(
    DWORD dwStyle,
    const RECT& rect,
    CWnd* pParentWnd,
    UINT nID);
```  
  
### <a name="parameters"></a>參數  
 `dwStyle`  
 指定索引標籤控制項的樣式。 套用的任何組合[索引標籤控制項樣式](http://msdn.microsoft.com/library/windows/desktop/bb760549)、 Windows SDK 中所述。 請參閱**備註**如需您也可以套用至控制項的視窗樣式的清單。  
  
 `rect`  
 指定索引標籤控制項的大小和位置。 它可以是[CRect](../../atl-mfc-shared/reference/crect-class.md)物件或[RECT](http://msdn.microsoft.com/library/windows/desktop/dd162897)結構。  
  
 `pParentWnd`  
 指定的索引標籤控制項的父視窗，通常`CDialog`。 它不得為**NULL**。  
  
 `nID`  
 指定索引標籤控制項的 id。  
  
### <a name="return-value"></a>傳回值  
 **TRUE**如果物件的初始化成功，否則為**FALSE**。  
  
### <a name="remarks"></a>備註  
 您建構`CTabCtrl`兩個步驟中的物件。 首先，呼叫建構函式，然後再呼叫**建立**，建立索引標籤控制項，並將它附加至`CTabCtrl`物件。  
  
 除了索引標籤控制項的樣式，您可以套用下列視窗樣式索引標籤控制項：  
  
- **WS_CHILD**建立表示索引標籤控制項的子視窗。 不能與`WS_POPUP`樣式。  
  
- **WS_VISIBLE**建立起始時是可見的索引標籤控制項。  
  
- **WS_DISABLED**建立視窗一開始停用。  
  
- **WS_GROUP**指定一組控制項所在使用者可以移動一個控制項到下一步 箭號索引鍵的第一個控制項。 所有控制項，以定義**WS_GROUP**樣式之後的第一個控制項必須屬於相同的群組。 下一個控制項與**WS_GROUP**樣式結束樣式的群組，並啟動下一個群組 （也就是說，一個群組結束開始下）。  
  
- **WS_TABSTOP**透過這些使用者可以使用 TAB 鍵移動的控制項的指定任意數目的其中一個。 TAB 鍵移至所指定的下一個控制項的使用者**WS_TABSTOP**樣式。  
  
 若要建立具有延伸的視窗樣式 索引標籤控制項，呼叫[CTabCtrl::CreateEx](#createex)而不是**建立**。  
  
### <a name="example"></a>範例  
 [!code-cpp[NVC_MFC_CTabCtrl#2](../../mfc/reference/codesnippet/cpp/ctabctrl-class_2.cpp)]  
  
##  <a name="createex"></a>CTabCtrl::CreateEx  
 建立控制項 （子視窗），並將它與相關聯`CTabCtrl`物件。  
  
```  
virtual BOOL CreateEx(
    DWORD dwExStyle,
    DWORD dwStyle,
    const RECT& rect,
    CWnd* pParentWnd,
    UINT nID);
```  
  
### <a name="parameters"></a>參數  
 `dwExStyle`  
 指定正在建立的控制項的延伸的樣式。 如需延伸的視窗樣式的清單，請參閱`dwExStyle`參數[CreateWindowEx](http://msdn.microsoft.com/library/windows/desktop/ms632680) Windows SDK 中。  
  
 `dwStyle`  
 指定索引標籤控制項的樣式。 套用的任何組合[索引標籤控制項樣式](http://msdn.microsoft.com/library/windows/desktop/bb760549)、 Windows SDK 中所述。 請參閱**備註**中[建立](#create)如需您也可以套用至控制項的視窗樣式的清單。  
  
 `rect`  
 若要參考[RECT](http://msdn.microsoft.com/library/windows/desktop/dd162897)結構描述的大小和位置來建立，用戶端座標中之視窗`pParentWnd`。  
  
 `pParentWnd`  
 為控制項的父視窗的指標。  
  
 `nID`  
 控制項的子視窗識別碼。  
  
### <a name="return-value"></a>傳回值  
 否則為 0，如果成功則為非零。  
  
### <a name="remarks"></a>備註  
 使用`CreateEx`而不是[建立](#create)套用延伸的視窗樣式，由 Windows 擴充的樣式序言**WS_EX_**。  
  
 `CreateEx`建立具有所指定的延伸視窗樣式控制項， `dwExStyle`。 設定擴充特定控制項使用的樣式[SetExtendedStyle](#setextendedstyle)。 例如，使用`CreateEx`設定做為這類樣式**WS_EX_CONTEXTHELP**，但使用`SetExtendedStyle`設定做為這類樣式**TCS_EX_FLATSEPARATORS**。 如需詳細資訊，請參閱中所述的樣式[ 索引標籤控制項擴充樣式](http://msdn.microsoft.com/library/windows/desktop/bb760546)Windows SDK 中。  
  
##  <a name="ctabctrl"></a>CTabCtrl::CTabCtrl  
 建構 `CTabCtrl` 物件。  
  
```  
CTabCtrl();
```  
  
##  <a name="deleteallitems"></a>CTabCtrl::DeleteAllItems  
 移除索引標籤控制項中的所有項目。  
  
```  
BOOL DeleteAllItems();
```  
  
### <a name="return-value"></a>傳回值  
 如果成功則為非零；否則為 0。  
  
##  <a name="deleteitem"></a>CTabCtrl::DeleteItem  
 從索引標籤控制項中移除指定的項目。  
  
```  
BOOL DeleteItem(int nItem);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 要刪除的項目以零為起始的值。  
  
### <a name="return-value"></a>傳回值  
 如果成功則為非零；否則為 0。  
  
### <a name="example"></a>範例  
 [!code-cpp[NVC_MFC_CTabCtrl#3](../../mfc/reference/codesnippet/cpp/ctabctrl-class_3.cpp)]  
  
##  <a name="deselectall"></a>CTabCtrl::DeselectAll  
 重設在索引標籤控制項中，清除已按下的任何項目。  
  
```  
void DeselectAll(BOOL fExcludeFocus);
```  
  
### <a name="parameters"></a>參數  
 *fExcludeFocus*  
 指定的項目取消選取範圍的旗標。 如果此參數設為**FALSE**，所有的索引標籤按鈕將會重設。 如果設定為**TRUE**，則除了目前所選取的所有索引標籤項目將會重設。  
  
### <a name="remarks"></a>備註  
 此成員函式實作的 Win32 訊息中，行為[TCM_DESELECTALL](http://msdn.microsoft.com/library/windows/desktop/bb760579)、 Windows SDK 中所述。  
  
##  <a name="drawitem"></a>CTabCtrl::DrawItem  
 當主控描繪索引標籤控制項變更的視覺外觀時，架構呼叫。  
  
```  
virtual void DrawItem(LPDRAWITEMSTRUCT lpDrawItemStruct);
```  
  
### <a name="parameters"></a>參數  
 `lpDrawItemStruct`  
 指標[DRAWITEMSTRUCT](http://msdn.microsoft.com/library/windows/desktop/bb775802)結構，描述要繪製的項目。  
  
### <a name="remarks"></a>備註  
 **ItemAction**隸屬`DRAWITEMSTRUCT`結構會定義要執行的繪圖動作。  
  
 根據預設，此成員函式沒有任何作用。 覆寫此成員函式，來實作主控描繪的繪圖`CTabCtrl`物件。  
  
 應用程式應該還原選取的顯示內容中提供所有的圖形裝置介面 (GDI) 物件`lpDrawItemStruct`之前此成員函式會結束。  
  
##  <a name="getcurfocus"></a>CTabCtrl::GetCurFocus  
 擷取具有目前焦點所在的索引標籤的索引。  
  
```  
int GetCurFocus() const;  
```  
  
### <a name="return-value"></a>傳回值  
 具有目前焦點所在的索引標籤以零為起始的索引。  
  
##  <a name="getcursel"></a>CTabCtrl::GetCurSel  
 擷取索引標籤控制項中目前選取的索引標籤。  
  
```  
int GetCurSel() const;  
```  
  
### <a name="return-value"></a>傳回值  
 選取的索引標籤，如果成功或-1，表示已不選取任何索引標籤的以零為起始的索引。  
  
##  <a name="getextendedstyle"></a>CTabCtrl::GetExtendedStyle  
 擷取目前正在使用的索引標籤控制項中的延伸的樣式。  
  
```  
DWORD GetExtendedStyle();
```  
  
### <a name="return-value"></a>傳回值  
 表示目前使用的索引標籤控制項中的延伸的樣式。 這個值是組合[索引標籤控制項擴充樣式](http://msdn.microsoft.com/library/windows/desktop/bb760546)、 Windows SDK 中所述。  
  
### <a name="remarks"></a>備註  
 此成員函式實作的 Win32 訊息行為[TCM_GETEXTENDEDSTYLE](http://msdn.microsoft.com/library/windows/desktop/bb760585)、 Windows SDK 中所述。  
  
##  <a name="getimagelist"></a>CTabCtrl::GetImageList  
 擷取與索引標籤控制項關聯的影像清單。  
  
```  
CImageList* GetImageList() const;  
```  
  
### <a name="return-value"></a>傳回值  
 如果成功，控制項影像清單索引標籤的指標否則， **NULL**。  
  
##  <a name="getitem"></a>CTabCtrl::GetItem  
 擷取索引標籤控制項中的索引標籤的相關資訊。  
  
```  
BOOL GetItem(int nItem,   TCITEM* pTabCtrlItem) const;  
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 以零為起始的索引標籤的索引。  
  
 `pTabCtrlItem`  
 指標[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554)用來指定要擷取之資訊的結構。 也可用來在索引標籤的相關資訊。此結構會搭配`InsertItem`， `GetItem`，和`SetItem`成員函式。  
  
### <a name="return-value"></a>傳回值  
 傳回**TRUE**如果登錄成功。**FALSE**否則。  
  
### <a name="remarks"></a>備註  
 當傳送訊息時，**遮罩**成員指定要傳回的屬性。 如果**遮罩**成員指定`TCIF_TEXT`值**pszText**成員必須包含接收項目文字的緩衝區的位址和**cchTextMax**成員必須指定緩衝區的大小。  
  
 **遮罩**  
 值，指定其`TCITEM`結構擷取或設定成員。 這個成員可以是零或下列值的組合：  
  
- `TCIF_TEXT`**PszText**成員是否有效。  
  
- `TCIF_IMAGE``iImage`成員是否有效。  
  
- `TCIF_PARAM`**LParam**成員是否有效。  
  
- `TCIF_RTLREADING`文字**pszText**希伯來文或阿拉伯文系統上使用由右至左讀取順序顯示。  
  
- `TCIF_STATE`**DwState**成員是否有效。  
  
 **pszText**  
 以 null 終止的字串，包含在索引標籤文字，如果結構包含一個索引標籤的相關資訊的指標。如果結構接收資訊，這個成員會指定接收在索引標籤文字的緩衝區的位址。  
  
 **cchTextMax**  
 所指向之緩衝區的大小**pszText**。 如果結構不能接收資訊時，會忽略這個成員。  
  
 `iImage`  
 如果沒有任何索引標籤的影像，索引索引標籤控制項影像清單，或-1。  
  
 **lParam**  
 [] 索引標籤相關聯的應用程式定義的資料。如果有四個位元組以上的應用程式定義的資料，每個索引標籤，應用程式必須定義的結構，並使用它，而不要`TCITEM`結構。 應用程式定義的結構中的第一個成員必須是[TCITEMHEADER](http://msdn.microsoft.com/library/windows/desktop/bb760556)結構。 **TCITEMHEADER**結構等同於`TCITEM`結構，但不含**lParam**成員。 您的結構大小的大小之間的差異**TCITEMHEADER**結構應該會等於每個索引標籤的額外位元組數目。  
  
### <a name="example"></a>範例  
 [!code-cpp[NVC_MFC_CTabCtrl#4](../../mfc/reference/codesnippet/cpp/ctabctrl-class_4.cpp)]  
  
##  <a name="getitemcount"></a>CTabCtrl::GetItemCount  
 擷取索引標籤控制項中的索引標籤數目。  
  
```  
int GetItemCount() const;  
```  
  
### <a name="return-value"></a>傳回值  
 索引標籤控制項中的項目數目。  
  
### <a name="example"></a>範例  
  請參閱範例的[CPropertySheet::GetTabControl](../../mfc/reference/cpropertysheet-class.md#gettabcontrol)。  
  
##  <a name="getitemrect"></a>CTabCtrl::GetItemRect  
 擷取指定之索引標籤索引標籤控制項中的週框。  
  
```  
BOOL GetItemRect(int nItem,   LPRECT lpRect) const;  
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 以零為起始的索引標籤項目索引。  
  
 `lpRect`  
 指標[RECT](http://msdn.microsoft.com/library/windows/desktop/dd162897)接收 索引標籤的周框的結構。這些座標會使用目前的對應模式在檢視區。  
  
### <a name="return-value"></a>傳回值  
 如果成功則為非零；否則為 0。  
  
### <a name="example"></a>範例  
  請參閱範例的[CPropertySheet::GetTabControl](../../mfc/reference/cpropertysheet-class.md#gettabcontrol)。  
  
##  <a name="getitemstate"></a>CTabCtrl::GetItemState  
 擷取所識別的索引標籤控制項項目狀態`nItem`。  
  
```  
DWORD GetItemState(
    int nItem,  
    DWORD dwMask) const;  
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 要擷取狀態資訊項目的以零為起始的索引編號。  
  
 `dwMask`  
 指定要傳回哪些項目的狀態旗標的遮罩。 如需值的清單，請參閱的遮罩成員[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554)結構，Windows SDK 中所述。  
  
### <a name="return-value"></a>傳回值  
 若要參考`DWORD`接收的狀態資訊的值。 可為下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**TCIS_BUTTONPRESSED**|選取索引標籤控制項項目。|  
|**TCIS_HIGHLIGHTED**|索引標籤控制項項目會反白顯示，而且索引標籤和文字則會使用目前的反白顯示色彩繪製。 使用時反白顯示色彩，這會是的則為 true 的插補，非遞色色彩。|  
  
### <a name="remarks"></a>備註  
 所指定項目的狀態**dwState**隸屬`TCITEM`結構。  
  
##  <a name="getrowcount"></a>CTabCtrl::GetRowCount  
 擷取目前的索引標籤控制項中的資料列數。  
  
```  
int GetRowCount() const;  
```  
  
### <a name="return-value"></a>傳回值  
 索引標籤控制項中的索引標籤的資料列數目。  
  
### <a name="remarks"></a>備註  
 只有索引標籤控制項具有**TCS_MULTILINE**樣式可以有多個資料列的索引標籤。  
  
##  <a name="gettooltips"></a>CTabCtrl::GetToolTips  
 擷取索引標籤控制項相關聯的工具提示控制項的控制代碼。  
  
```  
CToolTipCtrl* GetToolTips() const;  
```  
  
### <a name="return-value"></a>傳回值  
 如果成功; 時，工具提示控制項的控制代碼否則**NULL**。  
  
### <a name="remarks"></a>備註  
 如果有，索引標籤控制項建立工具提示控制項**TCS_TOOLTIPS**樣式。 您也可以指派至索引標籤控制項的工具提示控制項，使用`SetToolTips`成員函式。  
  
##  <a name="highlightitem"></a>CTabCtrl::HighlightItem  
 設定反白顯示的狀態索引標籤項目。  
  
```  
BOOL HighlightItem(int idItem,   BOOL fHighlight = TRUE);
```  
  
### <a name="parameters"></a>參數  
 `idItem`  
 以零為起始的索引標籤控制項項目索引。  
  
 `fHighlight`  
 值，指定要設定的反白顯示狀態。 如果此值為**TRUE**，[] 索引標籤會反白顯示; 如果**FALSE**，[] 索引標籤設為其預設狀態。  
  
### <a name="return-value"></a>傳回值  
 如果成功則不為零，否則為 0。  
  
### <a name="remarks"></a>備註  
 此成員函式實作的 Win32 訊息[TCM_HIGHLIGHTITEM](http://msdn.microsoft.com/library/windows/desktop/bb760602)、 Windows SDK 中所述。  
  
##  <a name="hittest"></a>CTabCtrl::HitTest  
 判斷哪些索引標籤上，如果有的話，位於指定的螢幕上的位置。  
  
```  
int HitTest(TCHITTESTINFO* pHitTestInfo) const;  
```  
  
### <a name="parameters"></a>參數  
 `pHitTestInfo`  
 指標[TCHITTESTINFO](http://msdn.microsoft.com/library/windows/desktop/bb760553)結構，在 Windows SDK 中，指定要測試的螢幕位置所述。  
  
### <a name="return-value"></a>傳回值  
 如果沒有索引標籤位於指定位置，傳回以零為起始的索引標籤或-1 索引。  
  
##  <a name="insertitem"></a>Ctabctrl:: Insertitem  
 現有的索引標籤控制項中插入新的索引標籤。  
  
```  
LONG InsertItem(
    int nItem,
    TCITEM* pTabCtrlItem);

 
LONG InsertItem(
    int nItem,
    LPCTSTR lpszItem);

 
LONG InsertItem(
    int nItem,
    LPCTSTR lpszItem,
    int nImage);

 
LONG InsertItem(
    UINT nMask,
    int nItem,
    LPCTSTR lpszItem,
    int nImage,
    LPARAM lParam);

 
LONG InsertItem(
    UINT nMask,  
    int nItem,  
    LPCTSTR lpszItem,  
    int nImage,  
    LPARAM lParam,  
    DWORD dwState,  
    DWORD dwStateMask);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 新的索引標籤的以零為起始的索引。  
  
 `pTabCtrlItem`  
 指標[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554)結構，指定索引標籤的屬性。  
  
 `lpszItem`  
 包含的文字 索引標籤的 null 結尾字串的位址。  
  
 `nImage`  
 插入影像清單中之影像的以零為起始的索引。  
  
 `nMask`  
 指定哪一個`TCITEM`結構要設定的屬性。 可以是零或下列值的組合：  
  
- `TCIF_TEXT`**PszText**成員是否有效。  
  
- `TCIF_IMAGE``iImage`成員是否有效。  
  
- `TCIF_PARAM`**LParam**成員是否有效。  
  
- `TCIF_RTLREADING`文字**pszText**希伯來文或阿拉伯文系統上使用由右至左讀取順序顯示。  
  
- `TCIF_STATE`**DwState**成員是否有效。  
  
 `lParam`  
 [] 索引標籤相關聯的應用程式定義的資料。  
  
 `dwState`  
 指定的項目狀態的值。 如需詳細資訊，請參閱[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554) Windows SDK 中。  
  
 *dwStateMask*  
 指定要設定哪些狀態。 如需詳細資訊，請參閱[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554) Windows SDK 中。  
  
### <a name="return-value"></a>傳回值  
 以零起始的索引，新的索引標籤，如果登錄成功。否則為-1。  
  
### <a name="example"></a>範例  
 [!code-cpp[NVC_MFC_CTabCtrl#5](../../mfc/reference/codesnippet/cpp/ctabctrl-class_5.cpp)]  
  
##  <a name="removeimage"></a>CTabCtrl::RemoveImage  
 索引標籤控制項影像清單中移除指定的映像。  
  
```  
void RemoveImage(int nImage);
```  
  
### <a name="parameters"></a>參數  
 `nImage`  
 要移除之影像的以零為起始索引。  
  
### <a name="remarks"></a>備註  
 此索引標籤控制項更新每個索引標籤的映像索引，好讓每個索引標籤會保持相同的映像相關聯。  
  
##  <a name="setcurfocus"></a>CTabCtrl::SetCurFocus  
 將焦點設定到索引標籤控制項中指定之索引標籤。  
  
```  
void SetCurFocus(int nItem);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 指定的索引標籤，取得焦點的索引。  
  
### <a name="remarks"></a>備註  
 此成員函式實作的 Win32 訊息行為[TCM_SETCURFOCUS](http://msdn.microsoft.com/library/windows/desktop/bb760610)、 Windows SDK 中所述。  
  
##  <a name="setcursel"></a>CTabCtrl::SetCurSel  
 索引標籤控制項中選取索引標籤。  
  
```  
int SetCurSel(int nItem);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 要選取的項目以零為起始的索引。  
  
### <a name="return-value"></a>傳回值  
 以零為起始的索引，先前選取的索引標籤，如果成功，否則為-1。  
  
### <a name="remarks"></a>備註  
 索引標籤控制項不會傳送**TCN_SELCHANGING**或**TCN_SELCHANGE**通知訊息時使用這個函式選取索引標籤。 這些通知會傳送使用**WM_NOTIFY**，當使用者按一下，或使用鍵盤來變更索引標籤。  
  
##  <a name="setextendedstyle"></a>CTabCtrl::SetExtendedStyle  
 設定索引標籤控制項的延伸的樣式。  
  
```  
DWORD SetExtendedStyle(DWORD dwNewStyle,   DWORD dwExMask = 0);
```  
  
### <a name="parameters"></a>參數  
 `dwNewStyle`  
 值，指定的索引標籤組合控制延伸的樣式。  
  
 `dwExMask`  
 A`DWORD`值，指出在哪些樣式`dwNewStyle`會受到影響。 只有在擴充的樣式`dwExMask`將會變更。 因為是，仍會維護所有其他樣式。 如果這個參數是零，則所有樣式中`dwNewStyle`會受到影響。  
  
### <a name="return-value"></a>傳回值  
 A`DWORD`值，包含先前[索引標籤控制項擴充樣式](http://msdn.microsoft.com/library/windows/desktop/bb760546)、 Windows SDK 中所述。  
  
### <a name="return-value"></a>傳回值  
 此成員函式實作的 Win32 訊息行為[TCM_SETEXTENDEDSTYLE](http://msdn.microsoft.com/library/windows/desktop/bb760627)、 Windows SDK 中所述。  
  
##  <a name="setimagelist"></a>CTabCtrl::SetImageList  
 指定索引標籤控制項影像清單。  
  
```  
CImageList* SetImageList(CImageList* pImageList);
```  
  
### <a name="parameters"></a>參數  
 `pImageList`  
 要指派給此索引標籤控制項影像清單的指標。  
  
### <a name="return-value"></a>傳回值  
 讓指標回到先前的影像清單或**NULL**如果沒有任何先前的影像清單。  
  
##  <a name="setitem"></a>CTabCtrl::SetItem  
 設定下列部分或所有索引標籤的屬性。  
  
```  
BOOL SetItem(int nItem,   TCITEM* pTabCtrlItem);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 項目的以零為起始的索引。  
  
 `pTabCtrlItem`  
 指標[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554)結構，其中包含新的項目屬性。 **遮罩**成員指定要設定的屬性。 如果**遮罩**成員指定`TCIF_TEXT`值**pszText**成員是以 null 結尾字串的位址和**cchTextMax**成員會被忽略。  
  
### <a name="return-value"></a>傳回值  
 如果成功則為非零；否則為 0。  
  
### <a name="example"></a>範例  
  請參閱範例的[GetItem](#getitem)。  
  
##  <a name="setitemextra"></a>CTabCtrl::SetItemExtra  
 設定每個索引標籤的索引標籤控制項中的應用程式定義的資料保留的位元組數目。  
  
```  
BOOL SetItemExtra(int nBytes);
```  
  
### <a name="parameters"></a>參數  
 `nBytes`  
 若要設定的額外位元組數目。  
  
### <a name="return-value"></a>傳回值  
 如果成功則不為零，否則為 0。  
  
### <a name="remarks"></a>備註  
 此成員函式實作的 Win32 訊息行為[TCM_SETITEMEXTRA](http://msdn.microsoft.com/library/windows/desktop/bb760633)、 Windows SDK 中所述。  
  
##  <a name="setitemsize"></a>CTabCtrl::SetItemSize  
 設定索引標籤控制項項目的寬度和高度。  
  
```  
CSize SetItemSize(CSize size);
```  
  
### <a name="parameters"></a>參數  
 `size`  
 索引標籤控制項項目的新寬度和高度 (以像素為單位)。  
  
### <a name="return-value"></a>傳回值  
 傳回索引標籤控制項項目的舊寬度和高度。  
  
##  <a name="setitemstate"></a>CTabCtrl::SetItemState  
 設定所識別的索引標籤控制項目狀態`nItem`。  
  
```  
BOOL SetItemState(
    int nItem,
    DWORD dwMask,
    DWORD dwState);
```  
  
### <a name="parameters"></a>參數  
 `nItem`  
 要設定的狀態資訊項目的以零為起始的索引編號。  
  
 `dwMask`  
 指定其中一個項目的狀態旗標，用於設定遮罩。 如需值的清單，請參閱的遮罩成員[TCITEM](http://msdn.microsoft.com/library/windows/desktop/bb760554)結構，Windows SDK 中所述。  
  
 `dwState`  
 若要參考`DWORD`值，其中包含狀態資訊。 可為下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**TCIS_BUTTONPRESSED**|選取索引標籤控制項項目。|  
|**TCIS_HIGHLIGHTED**|索引標籤控制項項目會反白顯示，而且索引標籤和文字則會使用目前的反白顯示色彩繪製。 使用時反白顯示色彩，這會是的則為 true 的插補，非遞色色彩。|  
  
### <a name="return-value"></a>傳回值  
 如果成功則為非零；否則為 0。  
  
##  <a name="setmintabwidth"></a>CTabCtrl::SetMinTabWidth  
 索引標籤控制項中設定的最小寬度的項目。  
  
```  
int SetMinTabWidth(int cx);
```  
  
### <a name="parameters"></a>參數  
 `cx`  
 索引標籤控制項項目設定的最小寬度。 如果這個參數設定為-1 時，控制項將使用的預設索引標籤的寬度。  
  
### <a name="return-value"></a>傳回值  
 先前的最小的索引標籤寬度。  
  
### <a name="return-value"></a>傳回值  
 此成員函式實作的 Win32 訊息行為[TCM_SETMINTABWIDTH](http://msdn.microsoft.com/library/windows/desktop/bb760637)、 Windows SDK 中所述。  
  
##  <a name="setpadding"></a>CTabCtrl::SetPadding  
 設定 （填補） 每個索引標籤的圖示和標籤控制項中的標籤周圍的空間數量。  
  
```  
void SetPadding(CSize size);
```  
  
### <a name="parameters"></a>參數  
 `size`  
 設定 （填補） 每個索引標籤的圖示和標籤控制項中的標籤周圍的空間數量。  
  
##  <a name="settooltips"></a>CTabCtrl::SetToolTips  
 將工具提示控制項指派給索引標籤控制項。  
  
```  
void SetToolTips(CToolTipCtrl* pWndTip);
```  
  
### <a name="parameters"></a>參數  
 `pWndTip`  
 工具提示控制項的控制代碼。  
  
### <a name="remarks"></a>備註  
 您可以取得工具提示控制項，藉由呼叫相關聯的索引標籤控制項`GetToolTips`。  
  
### <a name="example"></a>範例  
  請參閱範例的[CPropertySheet::GetTabControl](../../mfc/reference/cpropertysheet-class.md#gettabcontrol)。  
  
## <a name="see-also"></a>請參閱  
 [CWnd 類別](../../mfc/reference/cwnd-class.md)   
 [階層架構圖表](../../mfc/hierarchy-chart.md)   
 [CHeaderCtrl 類別](../../mfc/reference/cheaderctrl-class.md)   
 [CListCtrl 類別](../../mfc/reference/clistctrl-class.md)