---
title: _set_controlfp
ms.date: 04/05/2018
apiname:
- _set_controlfp
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
- api-ms-win-crt-runtime-l1-1-0.dll
apitype: DLLExport
f1_keywords:
- set_controlfp
- _set_controlfp
helpviewer_keywords:
- set_controlfp function
- floating-point functions, setting control word
- _set_controlfp function
ms.assetid: e0689d50-f68a-4028-a9c1-fb23eedee4ad
ms.openlocfilehash: 1187502f09849d7ca4d8e595c237cfa511d00c6b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62356677"
---
# <a name="setcontrolfp"></a>_set_controlfp

設定浮點控制字組。

## <a name="syntax"></a>語法

```C
void __cdecl _set_controlfp(
    unsigned int newControl,
    unsigned int mask
);
```

### <a name="parameters"></a>參數

*newControl*<br/>
新的控制字組位元值。

*mask*<br/>
要設定之新控制字組位元的遮罩。

## <a name="return-value"></a>傳回值

無。

## <a name="remarks"></a>備註

**_Set_controlfp**函數很相似 **_control87**，但它只會設定浮點控制字組*newControl*。 值中的位元表示浮點控制狀態。 浮點控制狀態可讓程式變更浮點數學套件中的精確度、四捨五入和無限大模式。 您也可以加上遮罩或取消遮罩浮點例外狀況，使用 **_set_controlfp**。 如需詳細資訊，請參閱 [_control87、_controlfp、\__control87_2](control87-controlfp-control87-2.md)。

進行編譯時，此函式已被取代[/clr （Common Language Runtime 編譯）](../../build/reference/clr-common-language-runtime-compilation.md)因為 common language runtime 只支援預設的浮點精確度。

## <a name="requirements"></a>需求

|常式傳回的值|必要的標頭|相容性|
|-------------|---------------------|-------------------|
|**_set_controlfp**|\<float.h>|僅限 x86 處理器|

如需相容性的詳細資訊，請參閱 [相容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>另請參閱

[浮點支援](../../c-runtime-library/floating-point-support.md)<br/>
[_clear87、_clearfp](clear87-clearfp.md)<br/>
[_status87、_statusfp、_statusfp2](status87-statusfp-statusfp2.md)<br/>
