---
title: is_assignable 類別
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::is_assignable
helpviewer_keywords:
- is_assignable
ms.assetid: 53444287-c8be-4ad2-9487-a85c066a4f84
ms.openlocfilehash: b1357bf8c5ad4dfd5035855e34a8fd6a7ed73d15
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62391006"
---
# <a name="isassignable-class"></a>is_assignable 類別

測試是否可將 `From` 類型的值指派給 `To` 類型。

## <a name="syntax"></a>語法

```cpp
template <class To, class From>
struct is_assignable;
```

### <a name="parameters"></a>參數

*若要*<br/>
接收指派的物件類型。

*From*<br/>
提供值的物件類型。

## <a name="remarks"></a>備註

未評估的運算式 `declval<To>() = declval<From>()` 必須格式正確。 兩者`From`並`To`必須是完整的類型**void**，或是界限未知的陣列。

## <a name="requirements"></a>需求

**標頭：**\<type_traits>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[<type_traits>](../standard-library/type-traits.md)<br/>
