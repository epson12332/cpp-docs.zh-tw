---
title: mbrlen
ms.date: 11/04/2016
apiname:
- mbrlen
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
- api-ms-win-crt-string-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- mbrlen
helpviewer_keywords:
- mbrlen function
ms.assetid: dde8dee9-e091-4c4c-81b3-639808885ae1
ms.openlocfilehash: ec9079b9b164e2b609a956ddf3a75cd42923bafc
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62156768"
---
# <a name="mbrlen"></a>mbrlen

判斷完成目前地區設定的多位元組字元所需的位元組數目，並提供在多位元組字元中間重新啟動的功能。

## <a name="syntax"></a>語法

```C
size_t mbrlen(
   const char * str,
   size_t count,
   mbstate_t * mbstate
);
```

### <a name="parameters"></a>參數

*str*<br/>
多位元組字元字串中要檢查的下一個位元組指標。

*count*<br/>
要檢查的最大位元組數目。

*mbstate*<br/>
目前移位狀態的初始位元組的指標*str*。

## <a name="return-value"></a>傳回值

下列其中一個值：

|||
|-|-|
0|下一步*計數*或更少個位元組會完成代表 null 字元的寬字元的多位元組字元。
1 到*計數*(含） 之間|下一步*計數*或更少個位元組會完成有效多位元組字元。 傳回的值是完成多位元組字元的位元組數目。
(size_t)(-2)|下一步*計數*個位元組會產生不完整但可能有效的多位元組字元和所有*計數*已處理的位元組。
(size_t)(-1)|發生編碼錯誤。 下一步*計數*或更少個位元組並不會提供完整且有效的多位元組字元。 在此情況下， **errno**設為 EILSEQ，且在轉換狀態*mbstate*未指定。

## <a name="remarks"></a>備註

**Mbrlen**函式最多會檢查*計數*位元組的位元組開始所指向*str*來判斷完成下一個所需的位元組數目多位元組字元，包括任何移位序列。 它相當於呼叫`mbrtowc(NULL, str, count, &mbstate)`何處*mbstate*是其中一個使用者提供**mbstate_t**物件或程式庫提供的靜態內部物件。

**Mbrlen**函式，儲存及使用中的不完整多位元組字元的移位狀態*mbstate*參數。 這可讓**mbrlen**多位元組字元中間重新啟動，如果需要檢查最*計數*位元組。 如果*mbstate*為 null 指標， **mbrlen**會使用內部靜態**mbstate_t**物件儲存移位狀態。 因為內部**mbstate_t**物件不是執行緒安全，我們建議您一律配置及傳遞您自己*mbstate*參數。

**Mbrlen**函式與不同[_mbclen、 mblen、 _mblen_l](mbclen-mblen-mblen-l.md)重新。 移位狀態會儲存在*mbstate*的後續呼叫相同或其他可重新啟動的函式。 混合使用可重新啟動和不可重新啟動之函式的結果不明。  例如，應用程式應該使用**wcsrlen**而不是**wcslen**如果後續呼叫**wcsrtombs**改用**wcstombs**.

### <a name="generic-text-routine-mappings"></a>一般文字常式對應

|TCHAR.H 常式|未定義 _UNICODE 和 _MBCS|_MBCS 已定義|_UNICODE 已定義|
|---------------------|------------------------------------|--------------------|-----------------------|
|不適用|不適用|**mbrlen**|不適用|

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**mbrlen**|\<wchar.h>|

如需其他相容性資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

此範例示範如何多位元組字元的解譯取決於目前的字碼頁，以及示範的繼續功能**mbrlen**。

```C
// crt_mbrlen.c
// Compile by using: cl crt_mbrlen.c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <locale.h>
#include <wchar.h>

size_t Example(const char * pStr)
{
    size_t      charLen = 0;
    size_t      charCount = 0;
    mbstate_t   mbState = {0};

    while ((charLen = mbrlen(pStr++, 1, &mbState)) != 0 &&
            charLen != (size_t)-1)
    {
        if (charLen != (size_t)-2) // if complete mbcs char,
        {
            charCount++;
        }
    }
    return (charCount);
}

int main( void )
{
    int         cp;
    size_t      charCount = 0;
    const char  *pSample =
        "\x82\xD0\x82\xE7\x82\xAA\x82\xC8: Shift-jis hiragana.";

    cp = _getmbcp();
    charCount = Example(pSample);
    printf("\nCode page: %d\n%s\nCharacter count: %d\n",
        cp, pSample, charCount);

    setlocale(LC_ALL, "ja-JP"); // Set Japanese locale
    _setmbcp(932); // and Japanese multibyte code page
    cp = _getmbcp();
    charCount = Example(pSample);
    printf("\nCode page: %d\n%s\nCharacter count: %d\n",
        cp, pSample, charCount);
}
```

```Output

Code page: 0
é╨éτé¬é╚: Shift-jis hiragana.
Character count: 29

Code page: 932
????: Shift-jis hiragana.
Character count: 25
```

## <a name="see-also"></a>另請參閱

[字串操作](../../c-runtime-library/string-manipulation-crt.md)<br/>
[地區設定](../../c-runtime-library/locale.md)<br/>
