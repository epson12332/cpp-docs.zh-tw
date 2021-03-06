---
title: _variant_t::Detach
ms.date: 11/04/2016
f1_keywords:
- _variant_t::Detach
- _variant_t.Detach
helpviewer_keywords:
- VARIANT object [C++], detatch
- Detach method [C++]
- VARIANT object
ms.assetid: c348ac08-62cf-4657-a16f-974a79c12158
ms.openlocfilehash: 719852c4556291747b612d54c44d4bf82caa9188
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62165927"
---
# <a name="varianttdetach"></a>_variant_t::Detach

**Microsoft 專屬**

中斷連結封裝`VARIANT`物件，這個`_variant_t`物件。

## <a name="syntax"></a>語法

```
VARIANT Detach( );
```

## <a name="return-value"></a>傳回值

封裝`VARIANT`。

## <a name="remarks"></a>備註

擷取並傳回封裝`VARIANT`，然後清除這個`_variant_t`而不會終結它的物件。 此成員函式移除`VARIANT`來自封裝和集合`VARTYPE`這個`_variant_t`物件設為 VT_EMPTY。 它可以決定是否要釋放傳回`VARIANT`藉由呼叫[VariantClear](/windows/desktop/api/oleauto/nf-oleauto-variantclear)函式。

**結束 Microsoft 專屬**

## <a name="see-also"></a>另請參閱

[_variant_t 類別](../cpp/variant-t-class.md)