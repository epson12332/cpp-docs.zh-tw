---
title: imaxabs
ms.date: 04/05/2018
apiname:
- imaxabs
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
- imaxabs
helpviewer_keywords:
- imaxabs function
ms.assetid: de2566a3-1415-4e9a-91b5-7ac3a49ebf5e
ms.openlocfilehash: a7492e08c3a078698292923ce395524ab5327ecf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62157489"
---
# <a name="imaxabs"></a>imaxabs

計算任何大小之整數的絕對值。

## <a name="syntax"></a>語法

```C
intmax_t imaxabs(
   intmax_t n
);
```

### <a name="parameters"></a>參數

*n*<br/>
整數值。

## <a name="return-value"></a>傳回值

**Imaxabs**函式會傳回引數的絕對值。 不會傳回錯誤。

> [!NOTE]
> 因為可以表示使用的負整數範圍**intmax_t**超過範圍的可表示的正整數，就可以提供的引數**imaxabs**無法轉換。 如果引數的絕對值無法由傳回類型，行為**imaxabs**是未定義。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|
|-------------|---------------------|
|**imaxabs**|\<inttypes.h>|

如需其他相容性資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>程式庫

所有版本的 [C 執行階段程式庫](../../c-runtime-library/crt-library-features.md)。

## <a name="example"></a>範例

```C
// crt_imaxabs.c
// Build using: cl /W3 /Tc crt_imaxabs.c
// This example calls imaxabs to compute an
// absolute value, then displays the results.

#include <stdio.h>
#include <stdlib.h>
#include <inttypes.h>

int main(int argc, char *argv[])
{
   intmax_t x = LLONG_MIN + 2;

   printf("The absolute value of %lld is %lld\n", x, imaxabs(x));
}
```

```Output
The absolute value of -9223372036854775806 is 9223372036854775806
```

## <a name="see-also"></a>另請參閱

[資料轉換](../../c-runtime-library/data-conversion.md)<br/>
[浮點支援](../../c-runtime-library/floating-point-support.md)<br/>
[abs、labs、llabs、_abs64](abs-labs-llabs-abs64.md)<br/>
[_cabs](cabs.md)<br/>
[fabs、fabsf、fabsl](fabs-fabsf-fabsl.md)<br/>
