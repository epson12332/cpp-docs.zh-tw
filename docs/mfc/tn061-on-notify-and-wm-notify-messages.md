---
title: "TN061: ON_NOTIFY 和 WM_NOTIFY 訊息 |Microsoft 文件"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: cpp-windows
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ON_NOTIFY
- WM_NOTIFY
dev_langs: C++
helpviewer_keywords:
- ON_NOTIFY_EX message [MFC]
- TN061
- ON_NOTIFY message [MFC]
- ON_NOTIFY_EX_RANGE message [MFC]
- ON_NOTIFY_RANGE message [MFC]
- notification messages
- WM_NOTIFY message
ms.assetid: 04a96dde-7049-41df-9954-ad7bb5587caf
caps.latest.revision: "9"
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: e8e8b8c806d03a1378998031453bffff85892086
ms.sourcegitcommit: ebec1d449f2bd98aa851667c2bfeb7e27ce657b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
---
# <a name="tn061-onnotify-and-wmnotify-messages"></a>TN061：ON_NOTIFY 和 WM_NOTIFY 訊息
> [!NOTE]
>  下列技術提示自其納入線上文件以來，未曾更新。 因此，有些程序和主題可能已過期或不正確。 如需最新資訊，建議您在線上文件索引中搜尋相關的主題。  
  
 這個技術提示提供背景資訊的新**WM_NOTIFY**訊息，並說明建議 （且最常見） 的方式處理**WM_NOTIFY** MFC 應用程式中的訊息。  
  
 **Windows 中的通知訊息 3.x**  
  
 在 Windows 3.x 中，控制項通知的事件，例如滑鼠點選其父系內容和選取項目和變更控制項背景繪製所傳送訊息給父代。 簡單的通知會傳送特殊**WM_COMMAND**訊息，以通知程式碼 (例如**BN_CLICKED**)，並控制封裝的識別碼`wParam`和控制項的控制代碼中`lParam`. 請注意，因為`wParam`和`lParam`是完整的沒有任何方法可以傳遞任何額外的資料，這些訊息可以是簡單的通知。 例如，在**BN_CLICKED**通知，沒有任何方法可以將資訊傳送滑鼠游標的位置時的 button 已按下。  
  
 在 Windows 3.x 不必傳送通知訊息，其中包含其他資料控制項，在使用時的特殊用途的訊息，包括各種`WM_CTLCOLOR`， `WM_VSCROLL`， `WM_HSCROLL`， `WM_DRAWITEM`， `WM_MEASUREITEM`， `WM_COMPAREITEM`，`WM_DELETEITEM`， `WM_CHARTOITEM`， `WM_VKEYTOITEM`，依此類推。 這些訊息可以反映至控制項傳送它們。 如需詳細資訊，請參閱[TN062: Windows 控制項訊息反映的](../mfc/tn062-message-reflection-for-windows-controls.md)。  
  
 **在 Win32 中的通知訊息**  
  
 對於存在於 Windows 3.1 的控制項，Win32 API 所使用的通知訊息所使用的大部分在 Windows 3.x。 不過，Win32 也會增加許多複雜的複雜控制項所支援的 Windows 3.x。 通常，這些控制項需要傳送包含其通知訊息的其他資料。 而不是加入新**WM_\*** 訊息的每個新的通知，需要額外的資料，在設計工具的 Win32 API 選擇加入只在一個訊息， **WM_NOTIFY**，這可以傳遞任何以標準化方式的其他資料的數量。  
  
 **WM_NOTIFY**訊息包含傳送訊息的控制項識別碼`wParam`和中的結構的指標`lParam`。 這個結構是**NMHDR**結構或有一些較大結構**NMHDR**結構做為其第一個成員。 請注意，因為**NMHDR**成員是第一次，此結構的指標可以當做指標給**NMHDR**或根據您對它所做的轉換較大的結構指標。  
  
 在大部分情況下，指標會指向較大的結構，您必須將其轉型，當您使用它。 在只有幾個通知中，例如，一般通知 (其名稱開頭**NM_**) 和工具提示控制項的**TTN_SHOW**和**TTN_POP**通知、 是**NMHDR**實際使用的結構。  
  
 **NMHDR**結構或初始成員包含的控制代碼和傳送的訊息和通知碼的控制項 ID (例如**TTN_SHOW**)。 格式**NMHDR**結構如下所示：  
  
```  
typedef struct tagNMHDR {  
    HWND hwndFrom;  
    UINT idFrom;  
    UINT code;  
} NMHDR;  
```  
  
 如**TTN_SHOW**訊息，**程式碼**成員會設定為**TTN_SHOW**。  
  
 大部分的通知會將指標傳遞至較大的結構，其中包含**NMHDR**結構做為其第一個成員。 例如，請考慮使用清單檢視控制項的結構**LVN_KEYDOWN**通知訊息，會在清單檢視控制項中按下按鍵時傳送。 指標會指向**LV_KEYDOWN**結構，定義如下所示：  
  
```  
typedef struct tagLV_KEYDOWN {  
    NMHDR hdr;     
    WORD wVKey;    
    UINT flags;    
} LV_KEYDOWN;  
```  
  
 請注意，因為**NMHDR**成員是第一次在此結構中，您要傳入的通知訊息中的指標可以轉換成指標**NMHDR**或指標**LV_KEYDOWN**.  
  
 **所有新的 Windows 控制項通用的通知**  
  
 有些通知通用於所有新的 Windows 控制項。 這些通知傳遞指標**NMHDR**結構。  
  
|通知程式碼|因為傳送|  
|-----------------------|------------------|  
|**NM_CLICK**|使用者已按下滑鼠左的按鈕控制項中|  
|**NM_DBLCLK**|在控制項中的使用者按兩下的滑鼠左鍵|  
|**NM_RCLICK**|使用者已按下滑鼠右按鈕控制項中|  
|**NM_RDBLCLK**|在控制項中的使用者按兩下的滑鼠按鈕|  
|**NM_RETURN**|使用者控制項擁有輸入焦點且按下 ENTER 鍵|  
|**NM_SETFOCUS**|控制項具有輸入的焦點|  
|**NM_KILLFOCUS**|控制項已遺失輸入的焦點|  
|**NM_OUTOFMEMORY**|控制項無法完成作業，因為沒有足夠的記憶體|  
  
##  <a name="_mfcnotes_on_notify.3a_.handling_wm_notify_messages_in_mfc_applications"></a>ON_NOTIFY： 處理 WM_NOTIFY 訊息在 MFC 應用程式  
 此函式`CWnd::OnNotify`處理通知訊息。 其預設實作會檢查通知處理常式，呼叫的訊息對應。 一般情況下，您不會覆寫`OnNotify`。 相反地，您提供的處理常式函式，並將該處理常式的訊息對應項目加入至主控視窗的類別的訊息對應。  
  
 ClassWizard，透過 ClassWizard 屬性工作表，可以建立`ON_NOTIFY`訊息對應項目，並提供基本架構的處理常式函式。 多個要進行簡化使用 ClassWizard 的詳細資訊，請參閱[訊息對應到函式](../mfc/reference/mapping-messages-to-functions.md)。  
  
 `ON_NOTIFY`訊息對應巨集具有下列語法：  
  
```  
 
ON_NOTIFY(
wNotifyCode  ,  
id  ,
    memberFxn)  
 
```  
  
 位置設為斜體的參數會取代：  
  
 `wNotifyCode`  
 通知訊息處理，這類的程式碼**LVN_KEYDOWN**。  
  
 `id`  
 傳送通知之控制項的子系識別碼。  
  
 `memberFxn`  
 此通知會傳送時所要呼叫此成員函式。  
  
 您的成員函式必須使用下列原型宣告：  
  
```  
 
afx_msg void  
memberFxn  
(NMHDR* 
pNotifyStruct  , LRESULT* result);

 
```  
  
## <a name="remarks"></a>備註  
 其中是設為斜體的參數：  
  
 `pNotifyStruct`  
 上一節中所述的通知結構指標。  
  
 *結果*  
 您設定指標的結果碼傳回之前。  
  
## <a name="example"></a>範例  
 若要指定您想要成員函式`OnKeydownList1`來處理**LVN_KEYDOWN**從訊息`CListCtrl`其識別碼是`IDC_LIST1`，您要用於訊息對應中加入下列 ClassWizard:  
  
```  
ON_NOTIFY(LVN_KEYDOWN,
    IDC_LIST1,
    OnKeydownList1)  
```  
  
 在上述範例中，ClassWizard 所提供的函式是：  
  
```  
void CMessageReflectionDlg::OnKeydownList1(NMHDR* pNMHDR, LRESULT* pResult)  
{  
    LV_KEYDOWN* pLVKeyDow = (LV_KEYDOWN*)pNMHDR; *// TODO: Add your control notification handler *//       code here  
 
 *pResult = 0;  
}  
```  
  
 請注意 ClassWizard 會自動提供的適當類型的指標。 您可以透過存取通知的結構`pNMHDR`或`pLVKeyDow`。  
  
##  <a name="_mfcnotes_on_notify_range"></a>ON_NOTIFY_RANGE  
 如果您需要處理相同**WM_NOTIFY**訊息的一組控制項，您可以使用**ON_NOTIFY_RANGE**而不是`ON_NOTIFY`。 比方說，您可能會有一組要執行的特定通知訊息的相同動作的按鈕。  
  
 當您使用**ON_NOTIFY_RANGE**，指定要由指定開始和結束範圍的子識別碼處理通知訊息的子識別碼的連續範圍。  
  
 不會處理 ClassWizard **ON_NOTIFY_RANGE**; 若要使用它時，您需要自行編輯訊息對應。  
  
 訊息對應項目，且函式原型**ON_NOTIFY_RANGE**如下：  
  
```  
 
ON_NOTIFY_RANGE(
wNotifyCode  ,   
id  ,   
idLast  ,
    memberFxn)  
 
```  
  
 位置設為斜體的參數會取代：  
  
 `wNotifyCode`  
 通知訊息處理，這類的程式碼**LVN_KEYDOWN**。  
  
 `id`  
 連續的識別項的範圍中的第一個識別項。  
  
 `idLast`  
 連續的識別項的範圍中的最後一個識別項。  
  
 `memberFxn`  
 此通知會傳送時所要呼叫此成員函式。  
  
 您的成員函式必須使用下列原型宣告：  
  
```  
 
afx_msg void  
memberFxn  
(UINT   
id  ,
    NMHDR* 
pNotifyStruct  ,
    LRESULT* result);

 
```  
  
## <a name="remarks"></a>備註  
 其中是設為斜體的參數：  
  
 `id`  
 傳送通知之控制項的子系識別碼。  
  
 `pNotifyStruct`  
 通知結構，如上面所述的指標。  
  
 *結果*  
 您設定指標的結果碼傳回之前。  
  
##  <a name="_mfcnotes_tn061_on_notify_ex.2c_.on_notify_ex_range"></a>ON_NOTIFY_EX ON_NOTIFY_EX_RANGE  
 如果您想要在通知中的多個物件至路由處理的訊息，您可以使用**ON_NOTIFY_EX** (或**ON_NOTIFY_EX_RANGE**) 而非`ON_NOTIFY`(或**ON_NOTIFY_RANGE**). 唯一的差別**EX**版本和規則的版本是成員函式呼叫的**EX**版本會傳回**BOOL** ，指出是否訊息處理應該繼續執行。 傳回**FALSE**從此函式可讓您處理在多個物件相同的訊息。  
  
 不會處理 ClassWizard **ON_NOTIFY_EX**或**ON_NOTIFY_EX_RANGE**; 如果您想要使用其中一個項目，您需要自行編輯訊息對應。  
  
 訊息對應項目，且函式原型**ON_NOTIFY_EX**和**ON_NOTIFY_EX_RANGE**如下。 參數的意義是一樣的非**EX**版本。  
  
```  
 
ON_NOTIFY_EX(
nCode  ,  
id  ,
    memberFxn) ON_NOTIFY_EX_RANGE(
wNotifyCode  ,   
id  ,   
idLast  ,
    memberFxn)  
 
```  
  
 這兩個以上的原型是一樣的：  
  
```  
 
afx_msg BOOL  
memberFxn  
(UINT   
id  ,
    NMHDR* 
pNotifyStruct  ,
    LRESULT* result);

 
```  
  
## <a name="remarks"></a>備註  
 在這兩種情況下，`id`保存傳送通知之控制項的子系識別碼。  
  
 您的函式必須傳回**TRUE**如果尚未完全處理通知訊息或**FALSE**其他物件中的命令路由，如果應該有機會處理訊息。  
  
## <a name="see-also"></a>另請參閱  
 [依數字的技術提示](../mfc/technical-notes-by-number.md)   
 [依分類區分的技術提示](../mfc/technical-notes-by-category.md)
