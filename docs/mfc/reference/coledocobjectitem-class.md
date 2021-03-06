---
title: COleDocObjectItem 類別
ms.date: 11/04/2016
f1_keywords:
- COleDocObjectItem
- AFXOLE/COleDocObjectItem
- AFXOLE/COleDocObjectItem::COleDocObjectItem
- AFXOLE/COleDocObjectItem::DoDefaultPrinting
- AFXOLE/COleDocObjectItem::ExecCommand
- AFXOLE/COleDocObjectItem::GetActiveView
- AFXOLE/COleDocObjectItem::GetPageCount
- AFXOLE/COleDocObjectItem::OnPreparePrinting
- AFXOLE/COleDocObjectItem::OnPrint
- AFXOLE/COleDocObjectItem::QueryCommand
- AFXOLE/COleDocObjectItem::Release
helpviewer_keywords:
- COleDocObjectItem [MFC], COleDocObjectItem
- COleDocObjectItem [MFC], DoDefaultPrinting
- COleDocObjectItem [MFC], ExecCommand
- COleDocObjectItem [MFC], GetActiveView
- COleDocObjectItem [MFC], GetPageCount
- COleDocObjectItem [MFC], OnPreparePrinting
- COleDocObjectItem [MFC], OnPrint
- COleDocObjectItem [MFC], QueryCommand
- COleDocObjectItem [MFC], Release
ms.assetid: d150d306-8fd3-4831-b06d-afbe71d8fc9b
ms.openlocfilehash: 382960b4dc4dcfa61c836a87044dd14585756174
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62225509"
---
# <a name="coledocobjectitem-class"></a>COleDocObjectItem 類別

實作主動式文件內含項目。

## <a name="syntax"></a>語法

```
class COleDocObjectItem : public COleClientItem
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[COleDocObjectItem::COleDocObjectItem](#coledocobjectitem)|建構`COleDocObject`項目。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[COleDocObjectItem::DoDefaultPrinting](#dodefaultprinting)|使用預設的印表機設定的容器應用程式的文件列印。|
|[COleDocObjectItem::ExecCommand](#execcommand)|執行使用者指定的命令。|
|[COleDocObjectItem::GetActiveView](#getactiveview)|擷取文件的現用檢視表。|
|[COleDocObjectItem::GetPageCount](#getpagecount)|擷取容器應用程式的文件中的頁數。|
|[COleDocObjectItem::OnPreparePrinting](#onprepareprinting)|準備容器應用程式的文件進行列印。|
|[COleDocObjectItem::OnPrint](#onprint)|容器應用程式的文件列印。|
|[COleDocObjectItem::QueryCommand](#querycommand)|查詢使用者介面事件所產生之一或多個命令的狀態。|
|[COleDocObjectItem::Release](#release)|釋放連接至 OLE 連結的項目並將它關閉，如果它已開啟。 不會終結用戶端項目。|

## <a name="remarks"></a>備註

在 MFC 中，主動式文件會處理方式類似一般、 就地編輯內嵌，但有下列差異：

- `COleDocument`-衍生的類別仍然會維護一份目前內嵌的項目; 不過，這些項目可能`COleDocObjectItem`-衍生的項目。

- 作用中主動式文件時，它會佔用整個工作區的檢視時就地啟用作用中。

- 主動式文件容器具有完整控制權**協助**功能表。

- **協助**功能表包含功能表項目，針對主動式文件容器和伺服器。

因為使用中文件容器擁有**幫助** 功能表中，容器會負責轉送伺服器**協助**功能表訊息至伺服器。 這項整合由`COleDocObjectItem`。

如需有關功能表合併和主動式文件啟用的詳細資訊，請參閱概觀[作用中的文件內含項目](../../mfc/active-document-containment.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CCmdTarget](../../mfc/reference/ccmdtarget-class.md)

[CDocItem](../../mfc/reference/cdocitem-class.md)

[COleClientItem](../../mfc/reference/coleclientitem-class.md)

`COleDocObjectItem`

## <a name="requirements"></a>需求

**標頭：** afxole.h

##  <a name="coledocobjectitem"></a>  COleDocObjectItem::COleDocObjectItem

呼叫此成員函式來初始化`COleDocObjectItem`物件。

```
COleDocObjectItem(COleDocument* pContainerDoc = NULL);
```

### <a name="parameters"></a>參數

*pContainerDoc*<br/>
指標`COleDocument`做為作用中的文件容器的物件。 這個參數必須是 NULL，以啟用 IMPLEMENT_SERIALIZE。 通常具有非 NULL 的文件指標建構 OLE 項目。

##  <a name="dodefaultprinting"></a>  COleDocObjectItem::DoDefaultPrinting

由架構呼叫以使用預設設定的文件。

```
static HRESULT DoDefaultPrinting(
    CView* pCaller,
    CPrintInfo* pInfo);
```

### <a name="parameters"></a>參數

*pCaller*<br/>
指標[CView](../../mfc/reference/cview-class.md)傳送列印命令的物件。

*pInfo*<br/>
指標[CPrintInfo](../../mfc/reference/cprintinfo-structure.md)描述列印工作的物件。

##  <a name="execcommand"></a>  COleDocObjectItem::ExecCommand

呼叫此成員函式來執行使用者所指定的命令。

```
HRESULT ExecCommand(
    DWORD nCmdID,
    DWORD nCmdExecOpt = OLECMDEXECOPT_DONTPROMPTUSER,
    const GUID* pguidCmdGroup = NULL);
```

### <a name="parameters"></a>參數

*nCmdID*<br/>
要執行的命令識別碼。 所識別的群組必須位於*pguidCmdGroup*。

*nCmdExecOpt*<br/>
指定命令執行的選項。 根據預設，設定，才能執行此命令不會提示使用者。 請參閱[OLECMDEXECOPT](/windows/desktop/api/docobj/ne-docobj-olecmdexecopt)如值的清單。

*pguidCmdGroup*<br/>
命令群組的唯一識別碼。 根據預設，null 值，指定標準的群組。 此命令中傳遞*nCmdID*必須屬於群組。

### <a name="return-value"></a>傳回值

傳回 S_OK，如果登錄成功。否則，傳回的其中一個下列的錯誤代碼。

|值|描述|
|-----------|-----------------|
|E_UNEXPECTED|發生意外的錯誤。|
|E_FAIL|發生錯誤。|
|E_NOTIMPL|表示 MFC 本身應該嘗試轉譯和分派命令。|
|OLECMDERR_E_UNKNOWNGROUP|*pguidCmdGroup*為非 NULL，但未指定可辨識的命令群組。|
|OLECMDERR_E_NOTSUPPORTED|*nCmdID*無法辨識為有效的命令群組 pGroup 中。|
|OLECMDERR_DISABLED|所識別的命令*nCmdID*已停用，而且無法執行。|
|OLECMDERR_NOHELP|呼叫端所識別的命令上要求協助*nCmdID*但沒有說明。|
|OLECMDERR_CANCELLED|使用者已取消執行。|

### <a name="remarks"></a>備註

*PguidCmdGroup*並*nCmdID*參數會共同唯一識別要叫用命令。 *NCmdExecOpt*參數會指定要採取的確切動作。

##  <a name="getactiveview"></a>  COleDocObjectItem::GetActiveView

呼叫以取得變數的指標，此成員函式`IOleDocumentView`目前作用中檢視的介面。

```
LPOLEDOCUMENTVIEW GetActiveView() const;
```

### <a name="return-value"></a>傳回值

指標[IOleDocumentView](/windows/desktop/api/docobj/nn-docobj-ioledocumentview)目前作用中檢視的介面。 如果沒有目前的檢視，則會傳回 NULL。

### <a name="remarks"></a>備註

上傳回的參考計數`IOleDocumentView`之前便會傳回此函式指標不會遞增。

##  <a name="getpagecount"></a>  COleDocObjectItem::GetPageCount

呼叫此成員函式可擷取的文件中的頁數。

```
BOOL GetPageCount(
    LPLONG pnFirstPage,
    LPLONG pcPages);
```

### <a name="parameters"></a>參數

*pnFirstPage*<br/>
文件的第一頁的數目指標。 可以是 NULL，表示呼叫端不需要這個數字。

*pcPages*<br/>
對文件中的頁面總數的指標。 可以是 NULL，表示呼叫端不需要這個數字。

### <a name="return-value"></a>傳回值

如果成功則為非零；否則為 0。

##  <a name="onprepareprinting"></a>  COleDocObjectItem::OnPreparePrinting

此成員函式會準備列印文件的架構所呼叫。

```
static BOOL OnPreparePrinting(
    CView* pCaller,
    CPrintInfo* pInfo,
    BOOL bPrintAll = TRUE);
```

### <a name="parameters"></a>參數

*pCaller*<br/>
指標[CView](../../mfc/reference/cview-class.md)傳送列印命令的物件。

*pInfo*<br/>
指標[CPrintInfo](../../mfc/reference/cprintinfo-structure.md)描述列印工作的物件。

*bPrintAll*<br/>
指定是否要列印整份文件。

### <a name="return-value"></a>傳回值

如果成功則為非零；否則為 0。

##  <a name="onprint"></a>  COleDocObjectItem::OnPrint

列印文件，架構會呼叫此成員函式。

```
static void OnPrint(
    CView* pCaller,
    CPrintInfo* pInfo,
    BOOL bPrintAll = TRUE);
```

### <a name="parameters"></a>參數

*pCaller*<br/>
正在傳送列印命令 CView 物件的指標。

*pInfo*<br/>
指標[CPrintInfo](../../mfc/reference/cprintinfo-structure.md)描述列印工作的物件。

*bPrintAll*<br/>
指定是否要列印整份文件。

##  <a name="querycommand"></a>  COleDocObjectItem::QueryCommand

查詢使用者介面事件所產生之一或多個命令的狀態。

```
HRESULT QueryCommand(
    ULONG nCmdID,
    DWORD* pdwStatus,
    OLECMDTEXT* pCmdText =NULL,
    const GUID* pguidCmdGroup =NULL);
```

### <a name="parameters"></a>參數

*nCmdID*<br/>
要查詢的命令識別碼。

*pdwStatus*<br/>
指標，傳回查詢結果的旗標。 如需可能值的清單，請參閱 < [OLECMDF](/windows/desktop/api/docobj/ne-docobj-olecmdf)。

*pCmdText*<br/>
指標[OLECMDTEXT](/windows/desktop/api/docobj/ns-docobj-_tagolecmdtext)結構中要傳回單一命令的名稱和狀態資訊。 可以是 NULL，表示呼叫端不需要這項資訊。

*pguidCmdGroup*<br/>
命令群組的唯一識別碼可以是 NULL，指定標準的群組。

### <a name="return-value"></a>傳回值

傳回值的完整清單，請參閱 < [IOleCommandTarget::QueryStatus](/windows/desktop/api/docobj/nf-docobj-iolecommandtarget-querystatus) Windows SDK 中。

### <a name="remarks"></a>備註

此成員函式會模擬[IOleCommandTarget::QueryStatus](/windows/desktop/api/docobj/nf-docobj-iolecommandtarget-querystatus)方法，在 Windows SDK 中所述。

##  <a name="release"></a>  COleDocObjectItem::Release

釋放連接至 OLE 連結的項目並將它關閉，如果它已開啟。 不會終結用戶端項目。

```
virtual void Release(OLECLOSE dwCloseOption = OLECLOSE_NOSAVE);
```

### <a name="parameters"></a>參數

*dwCloseOption*<br/>
旗標，指定已載入狀態恢復時，OLE 項目儲存在哪些情況之下。 如需可能值的清單，請參閱 < [COleClientItem::Close](../../mfc/reference/coleclientitem-class.md#close)。

### <a name="remarks"></a>備註

不會終結用戶端項目。

## <a name="see-also"></a>另請參閱

[MFC 範例 MFCBIND](../../overview/visual-cpp-samples.md)<br/>
[COleClientItem 類別](../../mfc/reference/coleclientitem-class.md)<br/>
[階層架構圖表](../../mfc/hierarchy-chart.md)<br/>
[COleClientItem 類別](../../mfc/reference/coleclientitem-class.md)<br/>
[CDocObjectServerItem 類別](../../mfc/reference/cdocobjectserveritem-class.md)
