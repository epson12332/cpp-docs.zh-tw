---
title: _lrotl、_lrotr
ms.date: 04/04/2018
apiname:
- _lrotl
- _lrotr
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
- api-ms-win-crt-utility-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- lrotr
- lrotl
- _lrotr
- _lrotl
helpviewer_keywords:
- lrotl function
- bits
- _lrotr function
- lrotr function
- rotating bits
- _lrotl function
- bits, rotating
ms.assetid: d42f295b-35f9-49d2-9ee4-c66896ffe68e
ms.openlocfilehash: 71ca61676e4551155f9f14e792c5c1cee65ddb7e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62156960"
---
# <a name="lrotl-lrotr"></a>_lrotl、_lrotr

旋轉位元向左 (**_lrotl**) 或向右 (**_lrotr**)。

## <a name="syntax"></a>語法

```C
unsigned long _lrotl( unsigned long value, int shift );
unsigned long _lrotr( unsigned long value, int shift );
```

### <a name="parameters"></a>參數

*value*<br/>
要旋轉的值。

*shift*<br/>
*value* 要移位的位元數。

## <a name="return-value"></a>傳回值

這兩個函式會傳回旋轉的值。 不會傳回錯誤。

## <a name="remarks"></a>備註

**_Lrotl**並 **_lrotr**函式旋轉*值*由*shift*位元。 **_lrotl**旋轉保留，到更高有效位元的值。 **_lrotr**旋轉值右邊的 往較高有效位元。 這兩個函式會將旋轉超出 *value* 一端的位元換行到另一端。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**_lrotl**， **_lrotr**|\<stdlib.h>|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>範例

```C
// crt_lrot.c

#include <stdlib.h>
#include <stdio.h>

int main( void )
{
   unsigned long val = 0x0fac35791;

   printf( "0x%8.8lx rotated left eight bits is 0x%8.8lx\n",
            val, _lrotl( val, 8 ) );
   printf( "0x%8.8lx rotated right four bits is 0x%8.8lx\n",
            val, _lrotr( val, 4 ) );
}
```

```Output
0xfac35791 rotated left eight bits is 0xc35791fa
0xfac35791 rotated right four bits is 0x1fac3579
```

## <a name="see-also"></a>另請參閱

[浮點支援](../../c-runtime-library/floating-point-support.md)<br/>
[_rotl、_rotl64、_rotr、_rotr64](rotl-rotl64-rotr-rotr64.md)<br/>
