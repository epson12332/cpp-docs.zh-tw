---
title: _get_timezone
ms.date: 11/04/2016
apiname:
- _get_timezone
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
- api-ms-win-crt-time-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _get_timezone
- get_timezone
helpviewer_keywords:
- time zones
- get_timezone function
- _get_timezone function
ms.assetid: 30ab0838-0ae9-4a2f-bfe6-a49ee443b21e
ms.openlocfilehash: 26cf8114ab766bdb394d2db9ad5842622a447bd1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62287439"
---
# <a name="gettimezone"></a>_get_timezone

擷取國際標準時間 (UTC) 和當地時間之間的時差，以秒為單位。

## <a name="syntax"></a>語法

```C
error_t _get_timezone(
    long* seconds
);
```

### <a name="parameters"></a>參數

*seconds*<br/>
UTC 與當地時間之間的時差，以秒為單位。

## <a name="return-value"></a>傳回值

如果成功，或在為零**errno**值發生錯誤。

## <a name="remarks"></a>備註

**_Get_timezone**函式會擷取之間的時差 UTC 與當地時間做為整數。 對太平洋標準時間而言，預設值為 28,800 秒 (晚 UTC 八小時)。

如果*秒*是**NULL**，無效參數處理常式會叫用，如中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md)。 如果允許繼續執行，此函式會將**errno**要**EINVAL** ，並傳回**EINVAL**。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_get_timezone**|\<time.h>|

如需詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>另請參閱

[時間管理](../../c-runtime-library/time-management.md)<br/>
[errno、_doserrno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)<br/>
[_get_daylight](get-daylight.md)<br/>
[_get_dstbias](get-dstbias.md)<br/>
[_get_tzname](get-tzname.md)<br/>
