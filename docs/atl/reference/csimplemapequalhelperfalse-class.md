---
title: CSimpleMapEqualHelperFalse Class
ms.date: 11/04/2016
f1_keywords:
- CSimpleMapEqualHelperFalse
- ATLSIMPCOLL/ATL::CSimpleMapEqualHelperFalse
- ATLSIMPCOLL/ATL::CSimpleMapEqualHelperFalse::IsEqualKey
- ATLSIMPCOLL/ATL::CSimpleMapEqualHelperFalse::IsEqualValue
helpviewer_keywords:
- CSimpleMapEqualHelperFalse class
ms.assetid: a873eea3-e130-45cc-a476-61ee79511c3b
ms.openlocfilehash: 9c4241049ad323047f06c0b29f946521f2c02167
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62277892"
---
# <a name="csimplemapequalhelperfalse-class"></a>CSimpleMapEqualHelperFalse Class

這個類別是 helper [CSimpleMap](../../atl/reference/csimplemap-class.md)類別。

## <a name="syntax"></a>語法

```
template <class TKey, class TVal>
class CSimpleMapEqualHelperFalse
```

## <a name="members"></a>成員

### <a name="public-methods"></a>公用方法

|名稱|描述|
|----------|-----------------|
|[CSimpleMapEqualHelperFalse::IsEqualKey](#isequalkey)|（靜態）測試兩個索引鍵相等。|
|[CSimpleMapEqualHelperFalse::IsEqualValue](#isequalvalue)|（靜態）會傳回 false。|

## <a name="remarks"></a>備註

此特性類別是補充`CSimpleMap`類別。 它提供一種方法來比較兩個項目中包含`CSimpleMap`物件，特別是兩個值的項目或兩個索引鍵的項目。

值比較一律會傳回 false，並且另外，呼叫`ATLASSERT`是 false，如果曾被參考的引數。 在等號比較測試不充分定義所在的情況下，這個類別可讓對應，其包含索引鍵/值組，以正確運作，大多數的方法，但在定義完善的方式，例如取決於比較的方法中失敗[CSimpleMap::FindVal](../../atl/reference/csimplemap-class.md#findval)。

## <a name="requirements"></a>需求

**標頭：** atlsimpcoll.h

##  <a name="isequalkey"></a>  CSimpleMapEqualHelperFalse::IsEqualKey

測試兩個索引鍵相等。

```
static bool IsEqualKey(const TKey& k1, const TKey& k2);
```

### <a name="parameters"></a>參數

*k1*<br/>
第一個索引鍵。

*k2*<br/>
第二個索引鍵。

### <a name="return-value"></a>傳回值

如果索引鍵相等，false 否則，就會傳回 true。

### <a name="remarks"></a>備註

這個方法會呼叫[CSimpleArrayEqualHelper](../../atl/reference/csimplearrayequalhelper-class.md)。

##  <a name="isequalvalue"></a>  CSimpleMapEqualHelperFalse::IsEqualValue

傳回 false。

```
static bool IsEqualValue(const TVal&, const TVal&);
```

### <a name="return-value"></a>傳回值

傳回 false。

### <a name="remarks"></a>備註

這個方法一律會傳回 false，而且會呼叫`ATLASSERT`是 false，如果曾被參考的引數。 目的`CSimpleMapEqualHelperFalse::IsEqualValue`是強制方法使用時有充分定義等號比較測試，以定義完善的方式失敗的比較。

## <a name="see-also"></a>另請參閱

[CSimpleMapEqualHelper 類別](../../atl/reference/csimplemapequalhelper-class.md)<br/>
[類別概觀](../../atl/atl-class-overview.md)
