---
title: AsWeak 函式
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- client/Microsoft::WRL::AsWeak
helpviewer_keywords:
- AsWeak function
ms.assetid: a6f10cfc-c1d6-4761-adb9-1a119cc99913
ms.openlocfilehash: 45df6332fccb2a22284eb6478c7554d87318ca78
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62398845"
---
# <a name="asweak-function"></a>AsWeak 函式

擷取指定執行個體的弱式參考。

## <a name="syntax"></a>語法

```cpp
template<typename T>
HRESULT AsWeak(
   _In_ T* p,
   _Out_ WeakRef* pWeak
);
```

### <a name="parameters"></a>參數

*T*<br/>
參數的類型指標*p*。

*p*<br/>
型別的執行個體。

*pWeak*<br/>
這項作業完成時，參數的弱式參考的指標*p*。

## <a name="return-value"></a>傳回值

S_ok 時，如果這項作業成功，否則，發生錯誤的 HRESULT，表示失敗的原因。

## <a name="requirements"></a>需求

**標頭：** client.h

**命名空間：** Microsoft:: wrl

## <a name="see-also"></a>另請參閱

[Microsoft::WRL 命名空間](microsoft-wrl-namespace.md)