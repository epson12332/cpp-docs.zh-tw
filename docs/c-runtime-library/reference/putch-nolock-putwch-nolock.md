---
title: _putch_nolock、_putwch_nolock
ms.date: 11/04/2016
apiname:
- _putwch_nolock
- _putch_nolock
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
- api-ms-win-crt-conio-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _putch_nolock
- _puttch_nolock
- putch_nolock
- putwch_nolock
- _putwch_nolock
helpviewer_keywords:
- putwch_nolock function
- puttch_nolock function
- characters, writing
- putch_nolock function
- _putch_nolock function
- _puttch_nolock function
- console, writing characters to
- _putwch_nolock function
ms.assetid: edbc811d-bac6-47fa-a872-fe4f3a1590b0
ms.openlocfilehash: 3b3ce1bb36e8a6d938ad620af21e8c1d3bc768db
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62358205"
---
# <a name="putchnolock-putwchnolock"></a>_putch_nolock、_putwch_nolock

將字元寫入至主控台，而不需要鎖定執行緒。

> [!IMPORTANT]
> 這個應用程式開發介面不能用於在 Windows 執行階段中執行的應用程式。 如需詳細資訊，請參閱 [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md) (通用 Windows 平台應用程式中不支援的 CRT 函式)。

## <a name="syntax"></a>語法

```C
int _putch_nolock(
int c
);
wint_t _putwch_nolock(
wchar_t c
);
```

### <a name="parameters"></a>參數

*C*<br/>
要輸出的字元。

## <a name="return-value"></a>傳回值

如果成功，則會傳回 *c*。 如果 **_putch_nolock** 失敗，則會傳回 **EOF**；如果 **_putwch_nolock** 失敗，則會傳回 **WEOF**。

## <a name="remarks"></a>備註

**_putch_nolock** 和 **_putwch_nolock** 分別與 **_putch** 和 **_putwch** 相同，不同之處在於不受保護，不能免於其他執行緒的干擾。 因為它們不會造成鎖定其他執行緒的額外負荷，所以可能會比較快。 這些函式只能用在安全執行緒內容 (例如單一執行緒應用程式) 或呼叫範圍已經處理執行緒隔離的地方。

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|Tchar.h 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_puttch_nolock**|**_putch_nolock**|**_putch_nolock**|**_putwch_nolock**|

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_putch_nolock**|\<conio.h>|
|**_putwch_nolock**|\<conio.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>程式庫

所有版本的 [C 執行階段程式庫](../../c-runtime-library/crt-library-features.md)。

## <a name="see-also"></a>另請參閱

[主控台和連接埠 I/O ](../../c-runtime-library/console-and-port-i-o.md)<br/>
[_cprintf、_cprintf_l、_cwprintf、_cwprintf_l](cprintf-cprintf-l-cwprintf-cwprintf-l.md)<br/>
[_getch、_getwch](getch-getwch.md)<br/>
