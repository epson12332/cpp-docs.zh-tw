---
title: _snscanf、_snscanf_l、_snwscanf、_snwscanf_l
ms.date: 11/04/2016
apiname:
- _snwscanf
- _snscanf_l
- _snscanf
- _snwscanf_l
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
apitype: DLLExport
f1_keywords:
- _snscanf
- _snscanf_l
- _snwscanf
- snscanf_l
- snscanf
- _sntscanf_l
- _sntscanf
- _snwscanf_l
- sntscanf_l
- sntscanf
- snwscanf
- snwscanf_l
helpviewer_keywords:
- snscanf_l function
- snwscanf function
- _sntscanf_l function
- sntscanf function
- _snwscanf_l function
- _sntscanf function
- _snscanf_l function
- sntscanf_l function
- strings [C++], reading data from
- snscanf function
- snwscanf_l function
- _snwscanf function
- reading data, strings
- strings [C++], reading
- _snscanf function
ms.assetid: da1ac890-f905-4cd7-954b-3c90957b5551
ms.openlocfilehash: ba80bec70bbb96c383d0bbe73ed52f30fb90b7ef
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62355402"
---
# <a name="snscanf-snscanfl-snwscanf-snwscanfl"></a>_snscanf、_snscanf_l、_snwscanf、_snwscanf_l

從字串讀取所指定長度的格式化資料。 這些函式已有更安全的版本可供使用，請參閱 [_snscanf_s、_snscanf_s_l、_snwscanf_s、_snwscanf_s_l](snscanf-s-snscanf-s-l-snwscanf-s-snwscanf-s-l.md)。

## <a name="syntax"></a>語法

```C
int __cdecl _snscanf(
   const char * input,
   size_t length,
   const char * format,
   ...
);
int __cdecl _snscanf_l(
   const char * input,
   size_t length,
   const char * format,
   locale_t locale,
   ...
);
int __cdecl _snwscanf(
   const wchar_t * input,
   size_t length,
   const wchar_t * format,
   ...
);
int __cdecl _snwscanf_l(
   const wchar_t * input,
   size_t length,
   const wchar_t * format,
   locale_t locale,
   ...
);
```

### <a name="parameters"></a>參數

*input*<br/>
要檢查的輸入字串。

*length*<br/>
要檢查的字元數*輸入*。

*格式*<br/>
一或多個格式指定名稱。

*...*<br/>
將用來儲存擷取自輸入字串中的格式規範的值的選擇性變數*格式*。

*locale*<br/>
要使用的地區設定。

## <a name="return-value"></a>傳回值

這兩個函式都會傳回成功轉換和指派的欄位數；傳回值不包含已讀取但未指派的欄位。 傳回值 0 表示未指派任何欄位。 傳回值是**EOF**錯誤或第一次轉換之前就到達的字串結尾。 如需詳細資訊，請參閱 [sscanf](sscanf-sscanf-l-swscanf-swscanf-l.md)。

如果*輸入*或*格式*會**NULL**指標，或如果*長度*小於或等於零，會叫用無效參數處理常式，為中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md)。 如果允許繼續執行，則這些函式會傳回**EOF**並設定**errno**來**EINVAL**。

如需這些錯誤碼和其他錯誤碼的資訊，請參閱 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>備註

此函式就像是**sscanf** ，差別在於它能夠指定固定的檢查從輸入字串的字元數。 如需詳細資訊，請參閱 [sscanf](sscanf-sscanf-l-swscanf-swscanf-l.md)。

使用這些函式的版本 **_l**尾碼都相同，只不過它們而不是目前執行緒的地區設定傳入的地區設定參數。

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|Tchar.h 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_sntscanf**|**_snscanf**|**_snscanf**|**_snwscanf**|
|**_sntscanf_l**|**_snscanf_l**|**_snscanf_l**|**_snwscanf_l**|

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_snscanf**， **_snscanf_l**|\<stdio.h>|
|**_snwscanf**， **_snwscanf_l**|\<stdio.h> 或 \<wchar.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

```C
// crt_snscanf.c
// compile with: /W3

#include <stdio.h>
int main( )
{
   char  str1[] = "15 12 14...";
   wchar_t  str2[] = L"15 12 14...";
   char  s1[3];
   wchar_t  s2[3];
   int   i;
   float fp;

   i = _snscanf( str1, 6,  "%s %f", s1, &fp); // C4996
   // Note: _snscanf is deprecated; consider using _snscanf_s instead
   printf("_snscanf converted %d fields: ", i);
   printf("%s and %f\n", s1, fp);

   i = _snwscanf( str2, 6,  L"%s %f", s2, &fp); // C4996
   // Note: _snwscanf is deprecated; consider using _snwscanf_s instead
   wprintf(L"_snwscanf converted %d fields: ", i);
   wprintf(L"%s and %f\n", s2, fp);
}
```

```Output
_snscanf converted 2 fields: 15 and 12.000000
_snwscanf converted 2 fields: 15 and 12.000000
```

## <a name="see-also"></a>另請參閱

[scanf 寬度規格](../../c-runtime-library/scanf-width-specification.md)<br/>
