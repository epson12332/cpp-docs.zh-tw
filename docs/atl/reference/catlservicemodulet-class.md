---
title: CAtlServiceModuleT 類別
ms.date: 05/06/2019
f1_keywords:
- CAtlServiceModuleT
- ATLBASE/ATL::CAtlServiceModuleT
- ATLBASE/ATL::CAtlServiceModuleT::CAtlServiceModuleT
- ATLBASE/ATL::CAtlServiceModuleT::Handler
- ATLBASE/ATL::CAtlServiceModuleT::InitializeSecurity
- ATLBASE/ATL::CAtlServiceModuleT::Install
- ATLBASE/ATL::CAtlServiceModuleT::IsInstalled
- ATLBASE/ATL::CAtlServiceModuleT::LogEvent
- ATLBASE/ATL::CAtlServiceModuleT::OnContinue
- ATLBASE/ATL::CAtlServiceModuleT::OnInterrogate
- ATLBASE/ATL::CAtlServiceModuleT::OnPause
- ATLBASE/ATL::CAtlServiceModuleT::OnShutdown
- ATLBASE/ATL::CAtlServiceModuleT::OnStop
- ATLBASE/ATL::CAtlServiceModuleT::OnUnknownRequest
- ATLBASE/ATL::CAtlServiceModuleT::ParseCommandLine
- ATLBASE/ATL::CAtlServiceModuleT::PreMessageLoop
- ATLBASE/ATL::CAtlServiceModuleT::RegisterAppId
- ATLBASE/ATL::CAtlServiceModuleT::Run
- ATLBASE/ATL::CAtlServiceModuleT::ServiceMain
- ATLBASE/ATL::CAtlServiceModuleT::SetServiceStatus
- ATLBASE/ATL::CAtlServiceModuleT::Start
- ATLBASE/ATL::CAtlServiceModuleT::Uninstall
- ATLBASE/ATL::CAtlServiceModuleT::Unlock
- ATLBASE/ATL::CAtlServiceModuleT::UnregisterAppId
- ATLBASE/ATL::CAtlServiceModuleT::WinMain
- ATLBASE/ATL::CAtlServiceModuleT::m_bService
- ATLBASE/ATL::CAtlServiceModuleT::m_dwThreadID
- ATLBASE/ATL::CAtlServiceModuleT::m_hServiceStatus
- ATLBASE/ATL::CAtlServiceModuleT::m_status
- ATLBASE/ATL::CAtlServiceModuleT::m_szServiceName
helpviewer_keywords:
- CAtlServiceModuleT class
ms.assetid: 8fc753ce-4a50-402b-9b4a-0a4ce5dd496c
ms.openlocfilehash: 1d44e356d907afcb261c0b4a765f8807bb54dc19
ms.sourcegitcommit: da32511dd5baebe27451c0458a95f345144bd439
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65221181"
---
# <a name="catlservicemodulet-class"></a>CAtlServiceModuleT 類別

這個類別會實作一項服務。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
template <class T, UINT nServiceNameID>
class ATL_NO_VTABLE CAtlServiceModuleT : public CAtlExeModuleT<T>
```

#### <a name="parameters"></a>參數

*T*<br/>
您的類別衍生自`CAtlServiceModuleT`。

*nServiceNameID*<br/>
服務資源識別碼。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CAtlServiceModuleT::CAtlServiceModuleT](#catlservicemodulet)|建構函式。|

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CAtlServiceModuleT::Handler](#handler)|服務處理常式。|
|[CAtlServiceModuleT::InitializeSecurity](#initializesecurity)|提供服務的安全性設定的預設值。|
|[CAtlServiceModuleT::Install](#install)|安裝並建立服務。|
|[CAtlServiceModuleT::IsInstalled](#isinstalled)|確認已安裝服務。|
|[CAtlServiceModuleT::LogEvent](#logevent)|寫入事件記錄檔。|
|[CAtlServiceModuleT::OnContinue](#oncontinue)|覆寫這個方法，以繼續服務。|
|[CAtlServiceModuleT::OnInterrogate](#oninterrogate)|覆寫這個方法，以查閱服務。|
|[CAtlServiceModuleT::OnPause](#onpause)|覆寫這個方法，以暫停服務。|
|[CAtlServiceModuleT::OnShutdown](#onshutdown)|覆寫此方法以關閉服務|
|[CAtlServiceModuleT::OnStop](#onstop)|覆寫這個方法，以停止服務|
|[CAtlServiceModuleT::OnUnknownRequest](#onunknownrequest)|覆寫此方法以處理未知的服務要求|
|[CAtlServiceModuleT::ParseCommandLine](#parsecommandline)|剖析命令列，並執行必要的註冊。|
|[CAtlServiceModuleT::PreMessageLoop](#premessageloop)|輸入訊息迴圈之前，立即會呼叫這個方法。|
|[CAtlServiceModuleT::RegisterAppId](#registerappid)|在登錄中註冊服務。|
|[CAtlServiceModuleT::Run](#run)|執行服務。|
|[CAtlServiceModuleT::ServiceMain](#servicemain)|呼叫由服務控制管理員中的方法。|
|[CAtlServiceModuleT::SetServiceStatus](#setservicestatus)|更新服務狀態。|
|[CAtlServiceModuleT::Start](#start)|由呼叫`CAtlServiceModuleT::WinMain`在服務啟動時。|
|[CAtlServiceModuleT::Uninstall](#uninstall)|停止並移除服務。|
|[CAtlServiceModuleT::Unlock](#unlock)|遞減服務的鎖定計數。|
|[CAtlServiceModuleT::UnregisterAppId](#unregisterappid)|從登錄中移除服務。|
|[CAtlServiceModuleT::WinMain](#winmain)|這個方法會實作來執行服務所需的程式碼。|

### <a name="public-data-members"></a>公用資料成員

|名稱|描述|
|----------|-----------------|
|[CAtlServiceModuleT::m_bService](#m_bservice)|表示在程式執行為服務旗標。|
|[CAtlServiceModuleT::m_dwThreadID](#m_dwthreadid)|儲存執行緒識別項的成員變數。|
|[CAtlServiceModuleT::m_hServiceStatus](#m_hservicestatus)|儲存目前的服務的狀態資訊結構的控制代碼的成員變數。|
|[CAtlServiceModuleT::m_status](#m_status)|儲存目前的服務的狀態資訊結構的成員變數。|
|[CAtlServiceModuleT::m_szServiceName](#m_szservicename)|正在註冊服務的名稱。|

## <a name="remarks"></a>備註

`CAtlServiceModuleT`衍生自[CAtlExeModuleT](../../atl/reference/catlexemodulet-class.md)，實作 ATL 服務模組。 `CAtlServiceModuleT` 提供命令列處理、 安裝、 註冊和移除的方法。 如果需要額外的功能，這些和其他方法可以被覆寫。

這個類別會取代過時[CComModule 類別](../../atl/reference/ccommodule-class.md)用在舊版的 ATL 請參閱[ATL 模組類別](../../atl/atl-module-classes.md)如需詳細資訊。

## <a name="inheritance-hierarchy"></a>繼承階層

[_ATL_MODULE](atl-typedefs.md#_atl_module)

[CAtlModule](../../atl/reference/catlmodule-class.md)

[CAtlModuleT](../../atl/reference/catlmodulet-class.md)

[CAtlExeModuleT](../../atl/reference/catlexemodulet-class.md)

`CAtlServiceModuleT`

## <a name="requirements"></a>需求

**標頭：** atlbase.h

##  <a name="catlservicemodulet"></a>  CAtlServiceModuleT::CAtlServiceModuleT

建構函式。

```
CAtlServiceModuleT() throw();
```

### <a name="remarks"></a>備註

初始化資料成員，並設定初始服務狀態。

##  <a name="handler"></a>  CAtlServiceModuleT::Handler

服務處理常式。

```
void Handler(DWORD dwOpcode) throw();
```

### <a name="parameters"></a>參數

*dwOpcode*<br/>
定義處理常式作業參數。 如需詳細資訊，請參閱 < 備註 >。

### <a name="remarks"></a>備註

這是要擷取的服務和問題的指示，例如停止的狀態或暫停的服務控制管理員 (SCM) 呼叫的程式碼。 SCM 會傳遞作業程式碼，如下所示，為`Handler`來指出應該執行的服務。

|作業的程式碼|意義|
|--------------------|-------------|
|SERVICE_CONTROL_STOP|停止服務。 覆寫方法[CAtlServiceModuleT::OnStop](#onstop)變更行為的 atlbase.h 中。|
|SERVICE_CONTROL_PAUSE|實作的使用者。 空白的方法會覆寫[CAtlServiceModuleT::OnPause](#onpause) atlbase.h 暫停服務中。|
|SERVICE_CONTROL_CONTINUE|實作的使用者。 空白的方法會覆寫[CAtlServiceModuleT::OnContinue](#oncontinue) atlbase.h 繼續服務中。|
|SERVICE_CONTROL_INTERROGATE|實作的使用者。 空白的方法會覆寫[CAtlServiceModuleT::OnInterrogate](#oninterrogate) atlbase.h 詢問服務中。|
|SERVICE_CONTROL_SHUTDOWN|實作的使用者。 空白的方法會覆寫[CAtlServiceModuleT::OnShutdown](#onshutdown) atlbase.h 關閉服務中。|

如果無法辨識作業程式碼，方法[CAtlServiceModuleT::OnUnknownRequest](#onunknownrequest)呼叫。

預設 ATL 產生服務只會處理停止指令。 如果 SCM 通過 stop 指令，服務會通知程式即將停止 SCM。 服務接著會呼叫`PostThreadMessage`quit 的訊息張貼至本身。 這將終止訊息迴圈，服務會完全關閉。

##  <a name="initializesecurity"></a>  CAtlServiceModuleT::InitializeSecurity

提供服務的安全性設定的預設值。

```
HRESULT InitializeSecurity() throw();
```

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="remarks"></a>備註

任何類別都衍生自`CAtlServiceModuleT`必須在衍生類別中實作這個方法。

呼叫中使用 PKT 層級驗證、 RPC_C_IMP_LEVEL_IDENTIFY 的模擬層級和適當的非 null 安全性描述元`CoInitializeSecurity`。

對於精靈所產生的非屬性化的服務的專案，這會在

[!code-cpp[NVC_ATL_Service#1](../../atl/reference/codesnippet/cpp/catlservicemodulet-class_1.cpp)]

針對屬性化的服務專案，這會在

[!code-cpp[NVC_ATL_ServiceAttrib#1](../../atl/reference/codesnippet/cpp/catlservicemodulet-class_2.cpp)]

##  <a name="install"></a>  CAtlServiceModuleT::Install

安裝並建立服務。

```
BOOL Install() throw();
```

### <a name="return-value"></a>傳回值

如果成功，則傳回 TRUE 失敗則為 FALSE。

### <a name="remarks"></a>備註

會安裝到服務控制管理員 (SCM) 資料庫的服務，並接著會建立服務物件。 如果無法建立服務，會顯示訊息方塊，此方法會傳回 FALSE。

##  <a name="isinstalled"></a>  CAtlServiceModuleT::IsInstalled

確認已安裝服務。

```
BOOL IsInstalled() throw();
```

### <a name="return-value"></a>傳回值

為 true，則會傳回服務是否已安裝，則為 FALSE 否則。

##  <a name="logevent"></a>  CAtlServiceModuleT::LogEvent

寫入事件記錄檔。

```
void __cdecl LogEvent(LPCTSTR pszFormat, ...) throw();
```

### <a name="parameters"></a>參數

*pszFormat*<br/>
要寫入事件記錄檔的字串。

*...*<br/>
要寫入事件記錄檔的選擇性額外字串。

### <a name="remarks"></a>備註

這個方法將詳細資料寫出至事件記錄檔，使用函式[ReportEvent](/windows/desktop/api/winbase/nf-winbase-reporteventa)。 如果沒有服務正在執行，則會將字串傳送至主控台。

##  <a name="m_bservice"></a>  CAtlServiceModuleT::m_bService

表示在程式執行為服務旗標。

```
BOOL m_bService;
```

### <a name="remarks"></a>備註

用來區別應用程式 EXE 服務 EXE。

##  <a name="m_dwthreadid"></a>  CAtlServiceModuleT::m_dwThreadID

儲存服務的執行緒識別項的成員變數。

```
DWORD m_dwThreadID;
```

### <a name="remarks"></a>備註

此變數會儲存目前執行緒的執行緒識別項。

##  <a name="m_hservicestatus"></a>  CAtlServiceModuleT::m_hServiceStatus

儲存目前的服務的狀態資訊結構的控制代碼的成員變數。

```
SERVICE_STATUS_HANDLE m_hServiceStatus;
```

### <a name="remarks"></a>備註

[SERVICE_STATUS](/windows/desktop/api/winsvc/ns-winsvc-_service_status)結構包含服務的相關資訊。

##  <a name="m_status"></a>  CAtlServiceModuleT::m_status

儲存目前的服務的狀態資訊結構的成員變數。

```
SERVICE_STATUS m_status;
```

### <a name="remarks"></a>備註

[SERVICE_STATUS](/windows/desktop/api/winsvc/ns-winsvc-_service_status)結構包含服務的相關資訊。

##  <a name="m_szservicename"></a>  CAtlServiceModuleT::m_szServiceName

正在註冊服務的名稱。

```
TCHAR [256] m_szServiceName;
```

### <a name="remarks"></a>備註

Null 結尾的字串會儲存服務的名稱。

##  <a name="oncontinue"></a>  CAtlServiceModuleT::OnContinue

覆寫這個方法，以繼續服務。

```
void OnContinue() throw();
```

##  <a name="oninterrogate"></a>  CAtlServiceModuleT::OnInterrogate

覆寫這個方法，以查閱服務。

```
void OnInterrogate() throw();
```

##  <a name="onpause"></a>  CAtlServiceModuleT::OnPause

覆寫這個方法，以暫停服務。

```
void OnPause() throw();
```

##  <a name="onshutdown"></a>  CAtlServiceModuleT::OnShutdown

覆寫這個方法，以關閉服務。

```
void OnShutdown() throw();
```

##  <a name="onstop"></a>  CAtlServiceModuleT::OnStop

覆寫這個方法，以停止服務。

```
void OnStop() throw();
```

##  <a name="onunknownrequest"></a>  CAtlServiceModuleT::OnUnknownRequest

覆寫此方法以處理服務無法辨識的要求。

```
void OnUnknownRequest(DWORD /* dwOpcode*/) throw();
```

### <a name="parameters"></a>參數

*dwOpcode*<br/>
保留的。

##  <a name="parsecommandline"></a>  CAtlServiceModuleT::ParseCommandLine

剖析命令列，並執行必要的註冊。

```
bool ParseCommandLine(LPCTSTR lpCmdLine, HRESULT* pnRetCode) throw();
```

### <a name="parameters"></a>參數

*lpCmdLine*<br/>
命令列。

*pnRetCode*<br/>
對應至註冊 （如果它發生） 的 HRESULT。

### <a name="return-value"></a>傳回值

成功時或在命令列中提供的 RGS 檔無法登錄為 false 則傳回 true。

### <a name="remarks"></a>備註

剖析命令列和註冊或取消註冊提供的 RGS 檔如有必要。 這個方法會呼叫[CAtlExeModuleT::ParseCommandLine](../../atl/reference/catlexemodulet-class.md#parsecommandline)檢查 **/RegServer**並 **/UnregServer**。 新增引數 **-/ 服務**會註冊服務。

##  <a name="premessageloop"></a>  CAtlServiceModuleT::PreMessageLoop

輸入訊息迴圈之前，立即會呼叫這個方法。

```
HRESULT PreMessageLoop(int nShowCmd) throw();
```

### <a name="parameters"></a>參數

*nShowCmd*<br/>
此參數會傳遞至[CAtlExeModuleT::PreMessageLoop](../../atl/reference/catlexemodulet-class.md#premessageloop)。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="remarks"></a>備註

覆寫這個方法來加入自訂初始化程式碼服務。

##  <a name="registerappid"></a>  CAtlServiceModuleT::RegisterAppId

在登錄中註冊服務。

```
inline HRESULT RegisterAppId(bool bService = false) throw();
```

### <a name="parameters"></a>參數

*bService*<br/>
必須註冊為服務，則為 true。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

##  <a name="run"></a>  CAtlServiceModuleT::Run

執行服務。

```
HRESULT Run(int nShowCmd = SW_HIDE) throw();
```

### <a name="parameters"></a>參數

*nShowCmd*<br/>
指定要顯示的視窗的方式。 這個參數可以是其中一個值所述[WinMain](/windows/desktop/api/winbase/nf-winbase-winmain)一節。 預設值是 SW_HIDE。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="remarks"></a>備註

在被呼叫之後`Run`呼叫[CAtlServiceModuleT::PreMessageLoop](#premessageloop)， [CAtlExeModuleT::RunMessageLoop](../../atl/reference/catlexemodulet-class.md#runmessageloop)，和[CAtlExeModuleT::PostMessageLoop](../../atl/reference/catlexemodulet-class.md#postmessageloop).

##  <a name="servicemain"></a>  CAtlServiceModuleT::ServiceMain

由服務控制管理員時，會呼叫這個方法。

```
void ServiceMain(DWORD dwArgc, LPTSTR* lpszArgv) throw();
```

### <a name="parameters"></a>參數

*dwArgc*<br/>
Argc 引數。

*lpszArgv*<br/>
Argv 引數。

### <a name="remarks"></a>備註

服務控制管理員 (SCM) 呼叫`ServiceMain`當您在控制台中開啟 服務應用程式，選取服務，並按一下 開始。

SCM 之後會呼叫`ServiceMain`，服務必須讓 SCM 處理常式函式。 此函式可讓 SCM 取得服務的狀態並傳遞 （例如暫停或停止） 的特定指示。 接著， [catlservicemodulet:: Run](#run)呼叫來執行服務的主要工作。 `Run` 會繼續執行，直到服務已停止。

##  <a name="setservicestatus"></a>  CAtlServiceModuleT::SetServiceStatus

這個方法會更新服務狀態。

```
void SetServiceStatus(DWORD dwState) throw();
```

### <a name="parameters"></a>參數

*dwState*<br/>
新的狀態。 請參閱[SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)可能的值。

### <a name="remarks"></a>備註

更新服務的服務控制管理員的狀態資訊。 它由呼叫[catlservicemodulet:: Run](#run)， [catlservicemodulet:: Servicemain](#servicemain)和其他處理常式方法。 狀態也會儲存在成員變數[CAtlServiceModuleT::m_status](#m_status)。

##  <a name="start"></a>  CAtlServiceModuleT::Start

由呼叫`CAtlServiceModuleT::WinMain`在服務啟動時。

```
HRESULT Start(int nShowCmd) throw();
```

### <a name="parameters"></a>參數

*nShowCmd*<br/>
指定要顯示的視窗的方式。 這個參數可以是其中一個值所述[WinMain](/windows/desktop/api/winbase/nf-winbase-winmain)一節。

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

### <a name="remarks"></a>備註

[CAtlServiceModuleT::WinMain](#winmain)方法會處理註冊和安裝，以及工作涉及移除登錄項目，並解除安裝模組。 當服務執行時，`WinMain`呼叫`Start`。

##  <a name="uninstall"></a>  CAtlServiceModuleT::Uninstall

停止並移除服務。

```
BOOL Uninstall() throw();
```

### <a name="return-value"></a>傳回值

如果成功，則傳回 TRUE 失敗則為 FALSE。

### <a name="remarks"></a>備註

停止執行服務，並從服務控制管理員資料庫中移除。

##  <a name="unlock"></a>  CAtlServiceModuleT::Unlock

遞減服務的鎖定計數。

```
LONG Unlock() throw();
```

### <a name="return-value"></a>傳回值

傳回的鎖定計數，這可能有助於診斷和偵錯。

##  <a name="unregisterappid"></a>  CAtlServiceModuleT::UnregisterAppId

從登錄中移除服務。

```
HRESULT UnregisterAppId() throw();
```

### <a name="return-value"></a>傳回值

會傳回 S_OK，如果成功或失敗的錯誤 HRESULT。

##  <a name="winmain"></a>  CAtlServiceModuleT::WinMain

這個方法會實作程式碼，以啟動服務。

```
int WinMain(int nShowCmd) throw();
```

### <a name="parameters"></a>參數

*nShowCmd*<br/>
指定要顯示的視窗的方式。 這個參數可以是其中一個值所述[WinMain](/windows/desktop/api/winbase/nf-winbase-winmain)一節。

### <a name="return-value"></a>傳回值

傳回服務的傳回值。

### <a name="remarks"></a>備註

這個方法會處理命令列 (與[CAtlServiceModuleT::ParseCommandLine](#parsecommandline))，然後啟動服務 (使用[catlservicemodulet:: Start](#start))。

## <a name="see-also"></a>另請參閱

[CAtlDllModuleT 類別](../../atl/reference/catlexemodulet-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)
