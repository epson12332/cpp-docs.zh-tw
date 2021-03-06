---
title: CRTThreadTraits 類別
ms.date: 11/04/2016
f1_keywords:
- CRTThreadTraits
- ATLBASE/ATL::CRTThreadTraits
- ATLBASE/ATL::CRTThreadTraits::CreateThread
helpviewer_keywords:
- CRTThreadTraits class
- threading [ATL], creation functions
- threading [ATL], CRT threads
ms.assetid: eb6e20b0-c2aa-4170-8e34-aaeeacc86343
ms.openlocfilehash: b5fa9273e3d24f5c912ebe30fab93baa6c9ff5c1
ms.sourcegitcommit: ecf274bcfe3a977c48745aaa243e5e731f1fdc5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66503159"
---
# <a name="crtthreadtraits-class"></a>CRTThreadTraits 類別

這個類別會提供建立函式的 CRT 往來文章。 如果執行緒會使用 CRT 函式，請使用這個類別。

> [!IMPORTANT]
>  此類別和其成員不能在 Windows 執行階段中執行的應用程式。

## <a name="syntax"></a>語法

```
class CRTThreadTraits
```

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CRTThreadTraits::CreateThread](#createthread)|（靜態）呼叫此函式來建立可以使用 CRT 函式的執行緒。|

## <a name="remarks"></a>備註

執行緒的特性是執行緒的提供特定類型建立函式的類別。 為 Windows 建立函式具有相同的簽章和語意[CreateThread](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createthread)函式。

下列類別會使用執行緒的特性：

- [CThreadPool](../../atl/reference/cthreadpool-class.md)

- [CWorkerThread](../../atl/reference/cworkerthread-class.md)

如果執行緒將不使用 CRT 函式，使用[Win32ThreadTraits](../../atl/reference/win32threadtraits-class.md)改。

## <a name="requirements"></a>需求

**標頭：** atlbase.h

##  <a name="createthread"></a>  CRTThreadTraits::CreateThread

呼叫此函式來建立可以使用 CRT 函式的執行緒。

```
static HANDLE CreateThread(
    LPSECURITY_ATTRIBUTES lpsa,
    DWORD dwStackSize,
    LPTHREAD_START_ROUTINE pfnThreadProc,
    void* pvParam,
    DWORD dwCreationFlags,
    DWORD* pdwThreadId) throw();
```

### <a name="parameters"></a>參數

*lpsa*<br/>
新的執行緒安全性屬性。

*dwStackSize*<br/>
新的執行緒堆疊大小。

*pfnThreadProc*<br/>
新執行緒的執行緒程序。

*pvParam*<br/>
要傳遞至執行緒程序的參數。

*dwCreationFlags*<br/>
建立旗標 （0 或 CREATE_SUSPENDED）。

*pdwThreadId*<br/>
[out]變數的位址 DWORD，成功時，接收新建立的執行緒的執行緒識別碼。

### <a name="return-value"></a>傳回值

傳回新建立的執行緒或 NULL 的控制代碼，在失敗。 呼叫[GetLastError](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)若要取得延伸錯誤資訊。

### <a name="remarks"></a>備註

請參閱[CreateThread](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createthread)更多有關此函數的參數。

此函式會呼叫[_beginthreadex](../../c-runtime-library/reference/beginthread-beginthreadex.md)建立執行緒。

## <a name="see-also"></a>另請參閱

[類別概觀](../../atl/atl-class-overview.md)
