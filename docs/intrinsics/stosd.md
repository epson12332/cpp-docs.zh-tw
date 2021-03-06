---
title: __stosd
ms.date: 11/04/2016
f1_keywords:
- __stosd
helpviewer_keywords:
- stosd instruction
- rep stosd instruction
- __stosd intrinsic
ms.assetid: 03104247-1cea-49f6-b6f8-287917bf5680
ms.openlocfilehash: 43a0efcfb94b7e53dacec16caccdacf86a96f5bb
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62390252"
---
# <a name="stosd"></a>__stosd

**Microsoft 專屬**

產生的存放區的字串指示 (`rep stosd`)。

## <a name="syntax"></a>語法

```
void __stosd(
   unsigned long* Dest,
   unsigned long Data,
   size_t Count
);
```

#### <a name="parameters"></a>參數

*目的地*<br/>
[out]作業的目的地。

*Data*<br/>
[in]要儲存的資料。

*計數*<br/>
[in]要寫入的雙字組的區塊的長度。

## <a name="requirements"></a>需求

|內建|架構|
|---------------|------------------|
|`__stosd`|x86、x64|

**標頭檔** \<intrin.h >

## <a name="remarks"></a>備註

結果是 doubleword`Data`寫入至區塊`Count`所指向的記憶體位置的雙字組`Dest`。

此常式僅可作為內建常式使用。

## <a name="example"></a>範例

```
// stosd.c
// processor: x86, x64

#include <stdio.h>
#include <memory.h>
#include <intrin.h>

#pragma intrinsic(__stosd)

int main()
{
    unsigned long val = 99999;
    unsigned long a[10];

    memset(a, 0, sizeof(a));
    __stosd(a+1, val, 2);

printf_s( "%u %u %u %u",
              a[0], a[1], a[2], a[3]);
}
```

```Output
0 99999 99999 0
```

**結束 Microsoft 專屬**

## <a name="see-also"></a>另請參閱

[編譯器內建](../intrinsics/compiler-intrinsics.md)