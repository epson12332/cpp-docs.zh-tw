---
title: _execvpe、_wexecvpe
ms.date: 11/04/2016
apiname:
- _execvpe
- _wexecvpe
apilocation:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-process-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- wexecvpe
- execvpe
- _wexecvpe
- _execvpe
helpviewer_keywords:
- wexecvpe function
- execvpe function
- _wexecvpe function
- _execvpe function
ms.assetid: c0c3c986-d9c0-4814-a96c-10f0b3092766
ms.openlocfilehash: 064f8b94a9a97795015c09c11cd56e0370dcc60c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62339399"
---
# <a name="execvpe-wexecvpe"></a>_execvpe、_wexecvpe

載入並執行新的子處理序。

> [!IMPORTANT]
> 這個應用程式開發介面不能用於在 Windows 執行階段中執行的應用程式。 如需詳細資訊，請參閱 [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md) (通用 Windows 平台應用程式中不支援的 CRT 函式)。

## <a name="syntax"></a>語法

```C
intptr_t _execvpe(
   const char *cmdname,
   const char *const *argv,
   const char *const *envp
);
intptr_t _wexecvpe(
   const wchar_t *cmdname,
   const wchar_t *const *argv,
   const wchar_t *const *envp
);
```

### <a name="parameters"></a>參數

*cmdname*<br/>
待執行檔案的路徑。

*argv*<br/>
參數指標的陣列。

*envp*<br/>
環境設定的指標陣列。

## <a name="return-value"></a>傳回值

如果成功的話，這些函式不會傳回呼叫處理序。 傳回值為-1 表示發生錯誤時，在此情況下**errno**設定全域變數。

|**errno**值|描述|
|-------------------|-----------------|
|**E2BIG**|引數和環境設定所需的空間超過 32 KB。|
|**EACCES**|指定的檔案具有鎖定或共用違規。|
|**EMFILE**|已開啟太多檔案。 (必須開啟指定的檔案，藉此判斷是否為可執行檔。)|
|**ENOENT**|找不到該檔案或路徑。|
|**ENOEXEC**|指定的檔案無法執行或可執行檔格式無效。|
|**ENOMEM**|沒有足夠的記憶體可用來執行新處理序；可用的記憶體已損毀；或存在無效的區塊，表示未正確配置呼叫的處理序。|

如需這些傳回碼和其他傳回碼的詳細資訊，請參閱 [errno、_doserrno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>備註

這些函式中的每一個都會載入和執行新處理序，並傳遞命令列引數的指標陣列和環境設定的指標陣列。 這些函式使用**路徑**環境變數尋找要執行的檔案。

**_Execvpe**函式會驗證其參數。 如果*cmdname*為 null 指標，或如果*argv*為 null 指標、 空陣列、 指標或陣列，其中包含作為第一個引數的空字串的指標，這些函式叫用無效參數處理常式，如中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md)。 如果允許繼續執行，這些函式會將**errno**要**EINVAL**並傳回-1。 未啟動任何處理序。

## <a name="requirements"></a>需求

|功能|必要的標頭|選擇性標頭|
|--------------|---------------------|---------------------|
|**_execvpe**|\<process.h>|\<errno.h>|
|**_wexecvpe**|\<process.h> 或 \<wchar.h>|\<errno.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

請參閱 [_exec、_wexec 函式](../../c-runtime-library/exec-wexec-functions.md)中的範例。

## <a name="see-also"></a>另請參閱

[流程控制和環境控制](../../c-runtime-library/process-and-environment-control.md)<br/>
[_exec、_wexec 函式](../../c-runtime-library/exec-wexec-functions.md)<br/>
[abort](abort.md)<br/>
[atexit](atexit.md)<br/>
[exit、_Exit、_exit](exit-exit-exit.md)<br/>
[_onexit、_onexit_m](onexit-onexit-m.md)<br/>
[_spawn、_wspawn 函式](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[system、_wsystem](system-wsystem.md)<br/>
