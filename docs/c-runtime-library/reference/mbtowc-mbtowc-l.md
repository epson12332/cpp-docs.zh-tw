---
title: mbtowc、_mbtowc_l
ms.date: 11/04/2016
apiname:
- mbtowc
- _mbtowc_l
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
- api-ms-win-crt-multibyte-l1-1-0.dll
- ntoskrnl.exe
apitype: DLLExport
f1_keywords:
- mbtowc
helpviewer_keywords:
- mbtowc function
- _mbtowc_l function
- mbtowc_l function
ms.assetid: dfd1c8a7-e73a-4307-9353-53b70b45d4d1
ms.openlocfilehash: c02d1a636db75b4a26891a93fa20327b7430443d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62156612"
---
# <a name="mbtowc-mbtowcl"></a>mbtowc、_mbtowc_l

將多位元組字元轉換為對應的寬字元。

## <a name="syntax"></a>語法

```C
int mbtowc(
   wchar_t *wchar,
   const char *mbchar,
   size_t count
);
int _mbtowc_l(
   wchar_t *wchar,
   const char *mbchar,
   size_t count,
   _locale_t locale
);
```

### <a name="parameters"></a>參數

*wchar*<br/>
寬字元的位址 (型別**wchar_t**)。

*mbchar*<br/>
位元組序列 (多位元組字元) 的位址。

*count*<br/>
要檢查的位元組數目。

*locale*<br/>
要使用的地區設定。

## <a name="return-value"></a>傳回值

如果**mbchar**不是**NULL**如果物件的*mbchar*指向有效的多位元組字元時，表單**mbtowc**傳回的長度多位元組字元的位元組。 如果*mbchar*是**NULL**或它所指向的物件是寬字元的 null 字元 (L '\0')，則函數會傳回 0。 如果物件的*mbchar*點不會構成有效的多位元組字元，在第一個*計數*字元，則傳回-1。

## <a name="remarks"></a>備註

**Mbtowc**函式會將*計數*或更少個位元組，指向*mbchar*的話*mbchar*不**NULL**，以對應的寬字元。 **mbtowc**會儲存在產生的寬字元*wchar*如果*wchar*不是**NULL**。 **mbtowc**不會檢查多個**MB_CUR_MAX**位元組。 **mbtowc**地區設定相關行為; 針對使用目前的地區設定 **_mbtowc_l**完全相同，只不過它會改用傳入的地區設定。 如需詳細資訊，請參閱 [Locale](../../c-runtime-library/locale.md)。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**mbtowc**|\<stdlib.h>|
|**_mbtowc_l**|\<stdlib.h>|

如需其他相容性資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>程式庫

所有版本的 [C 執行階段程式庫](../../c-runtime-library/crt-library-features.md)。

## <a name="example"></a>範例

```C
// crt_mbtowc.c
// Illustrates the behavior of the mbtowc function

#include <stdlib.h>
#include <stdio.h>

int main( void )
{
    int      i;
    char    *pmbc    = (char *)malloc( sizeof( char ) );
    wchar_t  wc      = L'a';
    wchar_t *pwcnull = NULL;
    wchar_t *pwc     = (wchar_t *)malloc( sizeof( wchar_t ) );
    printf( "Convert a wide character to multibyte character:\n" );
    wctomb_s( &i, pmbc, sizeof(char), wc );
    printf( "  Characters converted: %u\n", i );
    printf( "  Multibyte character: %x\n\n", *pmbc );

    printf( "Convert multibyte character back to a wide "
            "character:\n" );
    i = mbtowc( pwc, pmbc, MB_CUR_MAX );
    printf( "   Bytes converted: %u\n", i );
    printf( "   Wide character: %x\n\n", *pwc );
    printf( "Attempt to convert when target is NULL\n" );
    printf( "   returns the length of the multibyte character:\n" );
    i = mbtowc( pwcnull, pmbc, MB_CUR_MAX );
    printf( "   Length of multibyte character: %u\n\n", i );

    printf( "Attempt to convert a NULL pointer to a" );
    printf( " wide character:\n" );
    pmbc = NULL;
    i = mbtowc( pwc, pmbc, MB_CUR_MAX );
    printf( "   Bytes converted: %u\n", i );
}
```

```Output
Convert a wide character to multibyte character:
   Characters converted: 1
   Multibyte character: 61

Convert multibyte character back to a wide character:
   Bytes converted: 1
   Wide character: 61

Attempt to convert when target is NULL
   returns the length of the multibyte character:
   Length of multibyte character: 1

Attempt to convert a NULL pointer to a wide character:
   Bytes converted: 0
```

## <a name="see-also"></a>另請參閱

[資料轉換](../../c-runtime-library/data-conversion.md)<br/>
[MultiByteToWideChar](/windows/desktop/api/stringapiset/nf-stringapiset-multibytetowidechar)<br/>
[地區設定](../../c-runtime-library/locale.md)<br/>
[多位元組字元序列的解譯](../../c-runtime-library/interpretation-of-multibyte-character-sequences.md)<br/>
[_mbclen、mblen、_mblen_l](mbclen-mblen-mblen-l.md)<br/>
[wcstombs、_wcstombs_l](wcstombs-wcstombs-l.md)<br/>
[wctomb、_wctomb_l](wctomb-wctomb-l.md)<br/>
