---
title: '&lt;forward_list&gt; 函式'
ms.date: 11/04/2016
f1_keywords:
- forward_list/std::swap
ms.assetid: 0d6bc656-7049-4651-a4bd-c9a805e47756
ms.openlocfilehash: b425461f1428470b04a525efdd9a702ae038a283
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62159830"
---
# <a name="ltforwardlistgt-functions"></a>&lt;forward_list&gt; 函式

||
|-|
|[swap](#swap)|

## <a name="swap"></a>  swap

交換兩個轉送清單的項目。

```cpp
void swap(
    forward_list <Type, Allocator>& left,
    forward_list <Type, Allocator>& right);
```

### <a name="parameters"></a>參數

|參數|描述|
|---------------|-----------------|
|*left*|`forward_list` 類型的物件。|
|*right*|`forward_list` 類型的物件。|

### <a name="remarks"></a>備註

此範本函式會執行 `left.swap(right)`。

## <a name="see-also"></a>另請參閱

[<forward_list>](../standard-library/forward-list.md)<br/>
