---
title: is_nothrow_default_constructible 類別
ms.date: 11/04/2016
f1_keywords:
- type_traits/std::is_nothrow_default_constructible
helpviewer_keywords:
- is_nothrow_default_constructible
ms.assetid: c576fcc9-5be1-43aa-b93a-64d3f1848887
ms.openlocfilehash: d635c8a06d3acc45d214dbe7cb1eb7800f56dc86
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62148480"
---
# <a name="isnothrowdefaultconstructible-class"></a>is_nothrow_default_constructible 類別

測試類型是否有非擲回預設建構函式。

## <a name="syntax"></a>語法

```cpp
template <class Ty>
struct is_nothrow_default_constructible;
```

### <a name="parameters"></a>參數

*Ty*<br/>
要查詢的類型。

## <a name="remarks"></a>備註

如果型別述詞的執行個體保留 true 的型別*Ty* nothrow 預設建構函式，否則為 false。 類型述詞的執行個體相當於 `is_nothrow_constructible<Ty>`。

## <a name="requirements"></a>需求

**標頭：**\<type_traits>

**命名空間：** std

## <a name="see-also"></a>另請參閱

[<type_traits>](../standard-library/type-traits.md)<br/>
