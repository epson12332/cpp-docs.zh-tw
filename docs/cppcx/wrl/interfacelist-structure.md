---
title: InterfaceList 結構
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- implements/Microsoft::WRL::Details::InterfaceList
helpviewer_keywords:
- InterfaceList structure
ms.assetid: 6ec3228d-eb3e-4b7e-aef1-7dcf17bdf61a
ms.openlocfilehash: 745348e81888b5a87c57fbb99d397fcd423c3ee1
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62398208"
---
# <a name="interfacelist-structure"></a>InterfaceList 結構

支援 WRL 結構，而且不是直接從您的程式碼使用。

## <a name="syntax"></a>語法

```cpp
template <typename T, typename U>
struct InterfaceList;
```

### <a name="parameters"></a>參數

*T*<br/>
介面名稱;[遞迴] 清單中的第一個介面。

*U*<br/>
介面名稱;在 [遞迴] 清單中其餘的介面。

## <a name="remarks"></a>備註

用來建立介面的遞迴清單。

## <a name="members"></a>成員

### <a name="public-typedefs"></a>公用 Typedefs

|名稱|描述|
|----------|-----------------|
|`FirstT`|範本參數同義*T*。|
|`RestT`|範本參數同義*U*。|

## <a name="inheritance-hierarchy"></a>繼承階層

`InterfaceList`

## <a name="requirements"></a>需求

**標頭：** implements.h

**命名空間：** Microsoft::WRL::Details

## <a name="see-also"></a>另請參閱

[Microsoft::WRL::Details 命名空間](microsoft-wrl-details-namespace.md)