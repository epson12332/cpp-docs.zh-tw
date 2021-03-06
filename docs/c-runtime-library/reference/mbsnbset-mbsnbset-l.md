---
title: _mbsnbset、_mbsnbset_l
ms.date: 11/04/2016
apiname:
- _mbsnbset
- _mbsnbset_l
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
- api-ms-win-crt-multibyte-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- mbsnbset
- mbsnbset_l
- _mbsnbset
- _mbsnbset_l
helpviewer_keywords:
- tcsnset function
- _tcsnset_l function
- _mbsnbset function
- _tcsnset function
- _mbsnbset_l function
- mbsnbset_l function
- tcsnset_l function
- mbsnbset function
ms.assetid: 8e46ef75-9a56-42d2-a522-a08450c67c19
ms.openlocfilehash: 4c0f053cde32d71e4864c442b761606bb56c8829
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62331281"
---
# <a name="mbsnbset-mbsnbsetl"></a>_mbsnbset、_mbsnbset_l

設定第一個**n**個位元組的多位元組字元字串，為指定的字元。 這些函式已有更安全的版本可用，請參閱 [_mbsnbset_s、_mbsnbset_s_l](mbsnbset-s-mbsnbset-s-l.md)。

> [!IMPORTANT]
> 這個應用程式開發介面不能用於在 Windows 執行階段中執行的應用程式。 如需詳細資訊，請參閱 [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md) (通用 Windows 平台應用程式中不支援的 CRT 函式)。

## <a name="syntax"></a>語法

```C
unsigned char *_mbsnbset(
   unsigned char *str,
   unsigned int c,
   size_t count
);
unsigned char *_mbsnbset_l(
   unsigned char *str,
   unsigned int c,
   size_t count,
   _locale_t locale
);
```

### <a name="parameters"></a>參數

*str*<br/>
待變更字串。

*C*<br/>
單一位元組或多位元組字元的設定。

*count*<br/>
要設定的位元組數目。

*locale*<br/>
要使用的地區設定。

## <a name="return-value"></a>傳回值

**_mbsnbset**傳回變更後字串的指標。

## <a name="remarks"></a>備註

**_Mbsnbset**並 **_mbsnbset_l**函式會將，最多會第一個*計數*位元組*str*到*c*. 如果*計數*大於的長度*str*，長度*str*改用*計數*。 如果*c*是多位元組字元，而且無法設定完全讀入指定的最後一個位元組*計數*，最後一個位元組會以空白的字元填補。 **_mbsnbset**並 **_mbsnbset_l**並不會終止 null 結尾*str*。

**_mbsnbset**並 **_mbsnbset_l**類似 **_mbsnset**，只不過它會設定*計數*位元組而非*計數*字元*c*。

如果*str*是**NULL**或是*計數*為零，此函式會產生無效參數例外狀況，如中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md). 如果允許繼續，請執行**errno**設為**EINVAL**和函式會傳回**NULL**。 此外，如果*c*不是有效的多位元組字元， **errno**設定為**EINVAL**並改用一個空格。

輸出值會受到地區設定的 **LC_CTYPE** 分類設定影響；如需詳細資訊，請參閱 [setlocale](setlocale-wsetlocale.md)。 **_Mbsnbset**此函式版本會針對地區設定相關行為; 使用目前的地區設定 **_mbsnbset_l**版本也一樣，只不過它改用傳入的地區設定參數。 如需詳細資訊，請參閱 [Locale](../../c-runtime-library/locale.md)。

**安全性提示**：此 API 可能會帶來因緩衝區溢位問題所引發的威脅。 緩衝區滿溢問題是系統攻擊常見的方法，會造成權限無故提高。 如需詳細資訊，請參閱 [Avoiding Buffer Overruns (避免緩衝區滿溢)](/windows/desktop/SecBP/avoiding-buffer-overruns)。

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|Tchar.h 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tcsnset**|**_strnset**|**_mbsnbset**|**_wcsnset**|
|**_tcsnset_l**|**_strnset_l**|**_mbsnbset_l**|**_wcsnset_l**|

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_mbsnbset**|\<mbstring.h>|
|**_mbsnbset_l**|\<mbstring.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

```C
// crt_mbsnbset.c
// compile with: /W3
#include <mbstring.h>
#include <stdio.h>

int main( void )
{
   char string[15] = "This is a test";
   /* Set not more than 4 bytes of string to be *'s */
   printf( "Before: %s\n", string );
   _mbsnbset( string, '*', 4 ); // C4996
   // Note; _mbsnbset is deprecated; consider _mbsnbset_s
   printf( "After:  %s\n", string );
}
```

### <a name="output"></a>Output

```Output
Before: This is a test
After:  **** is a test
```

## <a name="see-also"></a>另請參閱

[字串操作](../../c-runtime-library/string-manipulation-crt.md)<br/>
[_mbsnbcat、_mbsnbcat_l](mbsnbcat-mbsnbcat-l.md)<br/>
[_strnset、_strnset_l、_wcsnset、_wcsnset_l、_mbsnset、_mbsnset_l](strnset-strnset-l-wcsnset-wcsnset-l-mbsnset-mbsnset-l.md)<br/>
[_strset、_strset_l、_wcsset、_wcsset_l、_mbsset、_mbsset_l](strset-strset-l-wcsset-wcsset-l-mbsset-mbsset-l.md)<br/>
