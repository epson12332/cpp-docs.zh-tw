---
title: VerifyInterfaceHelper 結構
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- implements/Microsoft::WRL::Details::VerifyInterfaceHelper
- implements/Microsoft::WRL::Details::VerifyInterfaceHelper::Verify
helpviewer_keywords:
- Microsoft::WRL::Details::VerifyInterfaceHelper structure
- Microsoft::WRL::Details::VerifyInterfaceHelper::Verify method
ms.assetid: ea95b641-199a-4fdf-964b-186b40cb3ba7
ms.openlocfilehash: cdd0272953b2399cd71efe207eb1c56e5de154e6
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62398091"
---
# <a name="verifyinterfacehelper-structure"></a>VerifyInterfaceHelper 結構

支援 Windows 執行階段C++樣板程式庫的基礎結構，不適合直接從您的程式碼使用。

## <a name="syntax"></a>語法

```cpp
template <bool isWinRTInterface, typename I>
struct VerifyInterfaceHelper;

template <typename I>
struct VerifyInterfaceHelper<false, I>;
```

### <a name="parameters"></a>參數

*I*<br/>
若要確認介面。

*isWinRTInterface*

## <a name="remarks"></a>備註

確認範本參數所指定的介面符合特定需求。

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

名稱                                            | 描述
----------------------------------------------- | ---------------------------------------------------------------------------------------------------
[VerifyInterfaceHelper::Verify 方法](#verify) | 確認目前的範本參數所指定的介面符合特定需求。

## <a name="inheritance-hierarchy"></a>繼承階層

`VerifyInterfaceHelper`

## <a name="requirements"></a>需求

**標頭：** implements.h

**命名空間：** Microsoft::WRL::Details

## <a name="verify"></a>VerifyInterfaceHelper::Verify

支援 WRL 結構，而且不是直接從您的程式碼使用。

```cpp
static void Verify();
```

### <a name="remarks"></a>備註

確認目前的範本參數所指定的介面符合特定需求。
