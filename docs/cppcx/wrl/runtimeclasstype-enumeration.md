---
title: RuntimeClassType 列舉
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- implements/Microsoft::WRL::RuntimeClassType
helpviewer_keywords:
- RuntimeClassType enumeration
ms.assetid: d380712d-672e-4ea9-b7c5-cf9fa7dbb770
ms.openlocfilehash: 80e8a120f7e3666721ff839a2a696388a64d734e
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62403124"
---
# <a name="runtimeclasstype-enumeration"></a>RuntimeClassType 列舉

指定的型別[RuntimeClass](runtimeclass-class.md)支援的執行個體。

## <a name="syntax"></a>語法

```cpp
enum RuntimeClassType;
```

## <a name="members"></a>成員

### <a name="values"></a>值

|名稱|描述|
|----------|-----------------|
|`ClassicCom`|傳統的 COM 執行階段類別。|
|`Delegate`|相當於 `ClassicCom`。|
|`InhibitFtmBase`|停用`FtmBase`支援，同時`__WRL_CONFIGURATION_LEGACY__`未定義。|
|`InhibitWeakReference`|停用弱式參考支援。|
|`WinRt`|Windows 執行階段類別。|
|`WinRtClassicComMix`|結合 `WinRt` 和 `ClassicCom`。|

## <a name="requirements"></a>需求

**標頭：** implements.h

**命名空間：** Microsoft:: wrl

## <a name="see-also"></a>另請參閱

[Microsoft::WRL 命名空間](microsoft-wrl-namespace.md)