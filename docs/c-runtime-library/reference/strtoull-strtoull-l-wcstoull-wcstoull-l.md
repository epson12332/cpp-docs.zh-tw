---
title: strtoull、_strtoull_l、wcstoull、_wcstoull_l
ms.date: 11/04/2016
apiname:
- _strtoull_l
- _wcstoull_l
- strtoull
- wcstoull
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
- api-ms-win-crt-convert-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- _wcstoull_l
- _tcstoull
- _tcstoull_l
- wcstoull
- _strtoull_l
- strtoull
helpviewer_keywords:
- strtoull function
- _tcstoull_l function
- _tcstoull function
- _wcstoull_l function
- _strtoull_l function
- wcstoull function
ms.assetid: 36dac1cc-e901-40a0-8802-63562d6d01df
ms.openlocfilehash: f23799b43a356600f48fb0fbf32b4604966c416b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62379203"
---
# <a name="strtoull-strtoulll-wcstoull-wcstoulll"></a>strtoull、_strtoull_l、wcstoull、_wcstoull_l

將字串轉換為不帶正負號的長整數值。

## <a name="syntax"></a>語法

```C
unsigned long long strtoull(
   const char *strSource,
   char **endptr,
   int base
);
unsigned long long _strtoull_l(
   const char *strSource,
   char **endptr,
   int base,
   _locale_t locale
);
unsigned long long wcstoull(
   const wchar_t *strSource,
   wchar_t **endptr,
   int base
);
unsigned long long _wcstoull_l(
   const wchar_t *strSource,
   wchar_t **endptr,
   int base,
   _locale_t locale
);
```

### <a name="parameters"></a>參數

*strSource*<br/>
以 Null 終止的待轉換字串。

*endptr*<br/>
停止掃描的字元指標。

*base*<br/>
要使用的數字基底。

*locale*<br/>
要使用的地區設定。

## <a name="return-value"></a>傳回值

**strtoull**傳回已轉換的值，如果有的話，或是**ULLONG_MAX**溢位。 **strtoull**會傳回 0，如果可以不執行任何轉換。 **wcstoull**傳回值類似**strtoull**。 這兩個函式中， **errno**設為**ERANGE**發生溢位或反向溢位。

如需傳回碼的詳細資訊，請參閱 [errno、_doserrno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>備註

所有這些函式都會將輸入的字串*strSource*要**不帶正負號****長****長**整數值。

**strtoull**停止讀取字串*strSource*它無法辨識為數字一部分的第一個字元。 這可能是終止的 null 字元，或是它可能會大於或等於第一個數字字元*基底*。 設定**LC_NUMERIC**分類的地區設定會決定在基底字元辨識*strSource*; 如需詳細資訊，請參閱[setlocale、 _wsetlocale](setlocale-wsetlocale.md). **strtoull**並**wcstoull**使用目前的地區設定，**_strtoull_l**並 **_wcstoull_l**改為使用傳入的地區設定，但相同。 如需詳細資訊，請參閱 [Locale](../../c-runtime-library/locale.md)。

如果*endptr*不是**NULL**，則停止掃描的字元指標會儲存在所指向的位置*endptr*。 如果可以不執行任何轉換 （找不到任何有效的數字或指定無效的基底） 的值*strSource*所指向的位置會儲存*endptr*。

**wcstoull**是寬字元版本的**strtoull**及其*strSource*引數是寬字元字串。 除此之外，這些函式的行為相同。

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|TCHAR.H 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tcstoull**|**strtoull**|**strtoull**|**wcstoull**|
|**_tcstoull_l**|**strtoull_l**|**_strtoull_l**|**_wcstoull_l**|

**strtoull**預期*strSource*指向下列格式的字串：

> [*whitespace*] [{**+** &#124; **-**}] [**0** [{ **x** &#124; **X** }]] [*digits*  &#124; *letters*]

A*空白字元*可能包含空格和定位字元字元，都會被忽略。 *數字*是一或多個十進位數字。 *字母*是一或多個字母 'a' 到 'z' （或 'A' 到 'Z'）。 不符合此格式的第一個字元會停止掃描。 如果*基底*是介於 2 到 36，則當成基底的數目。 如果*基底*為 0，所指向的字串起始字元*strSource*用來判斷基底。 如果第一個字元為 '0'，而第二個字元不是 'x' 或 X'，則字串會解譯為八進位整數。 如果第一個字元為 '0'，而第二個字元是 'x' 或 X'，則字串會解譯為十六進位整數。 如果第一個字元為 '1' 到 '9'，則字串會解譯為十進位整數。 字母 'a' 到 'z' (或 'A' 到 'Z') 被指派值 10 到 35，只允許指派值小於 *base* 的字母。 基底範圍外的第一個字元會停止掃描。 例如，如果*基底*為 0 和掃描的第一個字元是 '0'，假設為八進位整數，且 '8' 或 '9' 字元會停止掃描。 **strtoull**允許加號 (**+**) 或減號 (**-**) 前置詞，前置減號表示傳回的值為負數。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**strtoull**|\<stdlib.h>|
|**wcstoull**|\<stdlib.h> 或 \<wchar.h>|
|**_strtoull_l**|\<stdlib.h>|
|**_wcstoull_l**|\<stdlib.h> 或 \<wchar.h>|

如需其他相容性資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

請參閱 [strtod](strtod-strtod-l-wcstod-wcstod-l.md) 的範例。

## <a name="see-also"></a>另請參閱

[資料轉換](../../c-runtime-library/data-conversion.md)<br/>
[地區設定](../../c-runtime-library/locale.md)<br/>
[localeconv](localeconv.md)<br/>
[setlocale、_wsetlocale](setlocale-wsetlocale.md)<br/>
[字串轉換為數值函式](../../c-runtime-library/string-to-numeric-value-functions.md)<br/>
[strtod、_strtod_l、wcstod、_wcstod_l](strtod-strtod-l-wcstod-wcstod-l.md)<br/>
[strtol、wcstol、_strtol_l、_wcstol_l](strtol-wcstol-strtol-l-wcstol-l.md)<br/>
[strtoul、_strtoul_l、wcstoul、_wcstoul_l](strtoul-strtoul-l-wcstoul-wcstoul-l.md)<br/>
[strtoll、_strtoll_l、wcstoll、_wcstoll_l](strtoll-strtoll-l-wcstoll-wcstoll-l.md)<br/>
[atof、_atof_l、_wtof、_wtof_l](atof-atof-l-wtof-wtof-l.md)<br/>
