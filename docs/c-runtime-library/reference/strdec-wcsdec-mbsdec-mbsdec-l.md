---
title: _strdec、_wcsdec、_mbsdec、_mbsdec_l
ms.date: 11/04/2016
apiname:
- _wcsdec
- _strdec
- _mbsdec
- _mbsdec_l
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
- _strdec
- mbsdec_l
- strdec
- _mbsdec
- _mbsdec_l
- mbsdec
- wcsdec
- _wcsdec
helpviewer_keywords:
- mbsdec_l function
- mbsdec function
- tcsdec function
- _tcsdec function
- _strdec function
- _wcsdec function
- _mbsdec_l function
- strdec function
- wcsdec function
- _mbsdec function
ms.assetid: ae37c223-800f-48a9-ae8e-38c8d20af2dd
ms.openlocfilehash: 7e88bcf5bf7ffc5eba6feecd545cda8f7950829c
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62353874"
---
# <a name="strdec-wcsdec-mbsdec-mbsdecl"></a>_strdec、_wcsdec、_mbsdec、_mbsdec_l

將字串指標後移一個字元。

> [!IMPORTANT]
> **mbsdec**並**mbsdec_l**不能在 Windows 執行階段中執行的應用程式。 如需詳細資訊，請參閱 [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md) (通用 Windows 平台應用程式中不支援的 CRT 函式)。

## <a name="syntax"></a>語法

```C
unsigned char *_strdec(
   const unsigned char *start,
   const unsigned char *current
);
unsigned wchar_t *_wcsdec(
   const unsigned wchar_t *start,
   const unsigned wchar_t *current
);
unsigned char *_mbsdec(
   const unsigned char *start,
   const unsigned char *current
);
unsigned char *_mbsdec_l(
   const unsigned char *start,
   const unsigned char *current,
   _locale_t locale
);
```

### <a name="parameters"></a>參數

*start*<br/>
為任何字元的指標 (或 **_mbsdec**並 **_mbsdec_l**，任何多位元組字元的第一個位元組) 在來源字串中;*開始*前面必須加上*目前*來源字串中。

*current*<br/>
為任何字元的指標 (或 **_mbsdec**並 **_mbsdec_l**，任何多位元組字元的第一個位元組) 在來源字串中;*目前*必須遵循*開始*來源字串中。

*locale*<br/>
要使用的地區設定。

## <a name="return-value"></a>傳回值

**_mbsdec**， **_mbsdec_l**， **_strdec**，和 **_wcsdec**每個傳回的前置字元的指標*目前*;**_mbsdec**會傳回**NULL**如果的值*啟動*大於或等於*目前*。 **_tcsdec**會對應至其中一個這些函式和它的傳回值取決於此對應。

## <a name="remarks"></a>備註

**_Mbsdec**並 **_mbsdec_l**函式會傳回緊接在之前的多位元組字元的第一個位元組指標*目前*中包含的字串*啟動*。

輸出值的設定會影響**LC_CTYPE**地區設定分類設定; 請參閱[setlocale、 _wsetlocale](setlocale-wsetlocale.md)如需詳細資訊。  **_mbsdec**辨識多位元組字元序列，根據地區設定，目前正在使用中，雖然 **_mbsdec_l**完全相同，不同之處在於它改用傳入的地區設定參數。 如需詳細資訊，請參閱 [Locale](../../c-runtime-library/locale.md)。

如果*開始*或是*目前*會**NULL**，無效參數處理常式會叫用，如中所述[Parameter Validation](../../c-runtime-library/parameter-validation.md)。 如果允許繼續執行，則此函數會傳回**EINVAL**並設定**errno**來**EINVAL**。

> [!IMPORTANT]
> 這些函式可能容易受到緩衝區滿溢的威脅。 緩衝區滿溢可能被當成系統攻擊方式，因為它們可能導致非預期的提高權限。 如需詳細資訊，請參閱 [Avoiding Buffer Overruns (避免緩衝區滿溢)](/windows/desktop/SecBP/avoiding-buffer-overruns)。

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|Tchar.h 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tcsdec**|**_strdec**|**_mbsdec**|**_wcsdec**|

**_strdec**並 **_wcsdec**是單一位元組字元和寬字元版本的 **_mbsdec**並 **_mbsdec_l**。 **_strdec**並 **_wcsdec**只供此對應，否則應該不會使用。

如需詳細資訊，請參閱[使用泛型文字對應](../../c-runtime-library/using-generic-text-mappings.md)以及[泛型文字對應](../../c-runtime-library/generic-text-mappings.md)。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|選擇性標頭|
|-------------|---------------------|---------------------|
|**_mbsdec**|\<mbstring.h>|\<mbctype.h>|
|**_mbsdec_l**|\<mbstring.h>|\<mbctype.h>|
|**_strdec**|\<tchar.h>||
|**_wcsdec**|\<tchar.h>||

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

下列範例顯示的用法 **_tcsdec**。

```cpp
// crt_tcsdec.cpp
// Compile by using: cl /EHsc crt_tcsdec.cpp
#include <iostream>
#include <tchar.h>
using namespace std;

int main()
{
   const TCHAR *str = _T("12345");
   cout << "str: " << str << endl;

   const TCHAR *str2;
   str2 = str + 2;
   cout << "str2: " << str2 << endl;

   TCHAR *answer;
   answer = _tcsdec( str, str2 );
   cout << "answer: " << answer << endl;

   return (0);
}
```

下列範例顯示的用法 **_mbsdec**。

```cpp
// crt_mbsdec.cpp
// Compile by using: cl /EHsc crt_mbsdec.c
#include <iostream>
#include <mbstring.h>
using namespace std;

int main()
{
   char *str = "12345";
   cout << "str: " << str << endl;

   char *str2;
   str2 = str + 2;
   cout << "str2: " << str2 << endl;

   unsigned char *answer;
   answer = _mbsdec( reinterpret_cast<unsigned char *>( str ), reinterpret_cast<unsigned char *>( str2 ));

   cout << "answer: " << answer << endl;

   return (0);
}
```

## <a name="see-also"></a>另請參閱

[字串操作](../../c-runtime-library/string-manipulation-crt.md)<br/>
[_strinc、_wcsinc、_mbsinc、_mbsinc_l](strinc-wcsinc-mbsinc-mbsinc-l.md)<br/>
[_strnextc、_wcsnextc、_mbsnextc、_mbsnextc_l](strnextc-wcsnextc-mbsnextc-mbsnextc-l.md)<br/>
[_strninc、_wcsninc、_mbsninc、_mbsninc_l](strninc-wcsninc-mbsninc-mbsninc-l.md)<br/>
