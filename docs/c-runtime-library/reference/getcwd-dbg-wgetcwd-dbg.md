---
title: _getcwd_dbg、_wgetcwd_dbg
ms.date: 11/04/2016
apiname:
- _wgetcwd_dbg
- _getcwd_dbg
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
- api-ms-win-crt-environment-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _getcwd_dbg
- _wgetcwd_dbg
- getcwd_dbg
- wgetcwd_dbg
helpviewer_keywords:
- wgetcwd_dbg function
- working directory
- _getcwd_dbg function
- getcwd_dbg function
- current working directory
- _wgetcwd_dbg function
- directories [C++], current working
ms.assetid: 8d5d151f-d844-4aa6-a28c-1c11a22dc00d
ms.openlocfilehash: 9616c5f7e29b4f003d3943ba058d1f1a1d5adb5c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62287224"
---
# <a name="getcwddbg-wgetcwddbg"></a>_getcwd_dbg、_wgetcwd_dbg

偵錯版本的 [_getdcwd、_wgetdcwd](getcwd-wgetcwd.md) 函式 (僅於偵錯期間可供使用)。

## <a name="syntax"></a>語法

```C
char *_getcwd_dbg(
   char *buffer,
   int maxlen,
   int blockType,
   const char *filename,
   int linenumber
);
wchar_t *_wgetcwd_dbg(
   wchar_t *buffer,
   int maxlen,
   int blockType,
   const char *filename,
   int linenumber
);
```

### <a name="parameters"></a>參數

*buffer*<br/>
路徑的儲存位置。

*maxlen*<br/>
路徑以字元為單位的最大長度： **char**如 **_getcwd_dbg**並**wchar_t**如 **_wgetcwd_dbg**。

*blockType*<br/>
要求的記憶體區塊類型： **_CLIENT_BLOCK**或是 **_NORMAL_BLOCK**。

*filename*<br/>
要求配置作業之原始程式檔名稱的指標或**NULL**。

*linenumber*<br/>
其中要求配置作業，原始程式檔中的行號或**NULL**。

## <a name="return-value"></a>傳回值

將指標傳回至*緩衝區*。 A **NULL**傳回值表示錯誤，並**errno**設為**ENOMEM**，表示記憶體不足，無法配置*maxlen*位元組 (當**NULL**引數指定為*緩衝區*)，或**ERANGE**，表示路徑長度超過*maxlen*字元。

如需詳細資訊，請參閱 [errno、_doserrno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>備註

**_Getcwd_dbg**並 **_wgetcwd_dbg**函式 **_getcwd**並 **_wgetcwd**不同之處在於，當 **_偵錯**是定義，這些函式使用的偵錯版本**malloc**並 **_malloc_dbg**來配置記憶體**NULL**傳遞做為第一個參數。 如需詳細資訊，請參閱 [_malloc_dbg](malloc-dbg.md)。

在大多數情況中，您不需要明確地呼叫這些函式。 相反地，您可以定義 **_CRTDBG_MAP_ALLOC**旗標。 當 **_CRTDBG_MAP_ALLOC**定義，呼叫 **_getcwd**並 **_wgetcwd**重新對應至 **_getcwd_dbg**和 **_wgetcwd_dbg**分別與*blockType*設定為 **_NORMAL_BLOCK**。 因此，您不需要明確呼叫這些函式，除非您想要將標示為堆積區塊 **_CLIENT_BLOCK**。 如需詳細資訊，請參閱[偵錯堆積上的區塊類型](/visualstudio/debugger/crt-debug-heap-details)。

## <a name="generic-text-routine-mappings"></a>一般文字常式對應

|Tchar.h 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tgetcwd_dbg**|**_getcwd_dbg**|**_getcwd_dbg**|**_wgetcwd_dbg**|

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_getcwd_dbg**|\<crtdbg.h>|
|**_wgetcwd_dbg**|\<crtdbg.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>另請參閱

[_getcwd、_wgetcwd](getcwd-wgetcwd.md)<br/>
[目錄控制](../../c-runtime-library/directory-control.md)<br/>
[堆積配置函式的偵錯版本](/visualstudio/debugger/debug-versions-of-heap-allocation-functions)<br/>
