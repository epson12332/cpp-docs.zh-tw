---
title: trunc、truncf、truncl
ms.date: 04/05/2018
apiname:
- trunc
- truncf
- truncl
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
- api-ms-win-crt-math-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- trunc
- truncf
- truncl
- math/trunc
- math/truncf
- math/truncl
helpviewer_keywords:
- trunc function
- truncf function
- truncl function
ms.assetid: de2038ac-ac0b-483e-870c-e8992dcd4fd0
ms.openlocfilehash: 6e023b9d894ea1b40a0e056e73b7c32f1e3cbed7
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62268932"
---
# <a name="trunc-truncf-truncl"></a>trunc、truncf、truncl

判斷小於或等於指定浮點值且最接近的整數。

## <a name="syntax"></a>語法

```C
double trunc( double x );
float trunc( float x ); //C++ only
long double truncl( long double x );
```

```cpp
long double trunc( long double x ); //C++ only
float trunc( float x ); //C++ only
```

### <a name="parameters"></a>參數

*x*<br/>
要截斷的值。

## <a name="return-value"></a>傳回值

如果成功，傳回的整數值*x*、 朝向零四捨五入。

否則，可能會傳回下列其中一項：

|問題|Return|
|-----------|------------|
|*x* = ±INFINITY|x|
|*x* =  ±0|x|
|*x* = NaN|NaN|

依 [_matherr](matherr.md) 中的指定回報錯誤。

## <a name="remarks"></a>備註

因為C++允許多載，您可以呼叫多載**trunc**採用並傳回**float**並**長** **double**類型。 在 C 程式中， **trunc**一律採用並傳回**double**。

因為浮點數的最大值是確切的整數，這個函式本身不會溢位。 不過，您可能會因為將值傳回到整數類型而造成函式溢位。

您也可以透過隱含地從浮點數轉換為整數進行無條件捨去。不過，這麼做受限於可以用目標類型儲存的值。

## <a name="requirements"></a>需求

|功能|C 標頭|C++ 標頭|
|--------------|--------------|------------------|
|**trunc**， **truncf**， **truncl**|\<math.h>|\<cmath>|

如需其他相容性資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>另請參閱

[依字母順序排列的函式參考](crt-alphabetical-function-reference.md)<br/>
[floor、floorf、floorl](floor-floorf-floorl.md)<br/>
[ceil、ceilf、ceill](ceil-ceilf-ceill.md)<br/>
[round、roundf、roundl](round-roundf-roundl.md)<br/>
