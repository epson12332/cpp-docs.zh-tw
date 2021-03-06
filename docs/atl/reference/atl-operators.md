---
title: ATL 運算子
ms.date: 11/04/2016
helpviewer_keywords:
- operators [ATL]
ms.assetid: 58ccd252-2869-45ee-8a5c-3ca40ee7f8a2
ms.openlocfilehash: 6f1bd4f88b8d3a37f051a208a887c5264f61955a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62260905"
---
# <a name="atl-operators"></a>ATL 運算子

此章節包含 ATL 全域運算子參考主題。

|運算子|描述|
|--------------|-----------------|
|[operator ==](#operator_eq_eq)|比較兩個`CSid`物件或`SID`結構是否相等。|
|[operator !=](#operator_neq)|比較兩個`CSid`物件或`SID`結構是否不相等。|
|[operator <](#operator_lt)|測試是否`CSid`物件或`SID`運算子左邊的結構是小於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。|
|[operator >](#operator_gt)|測試是否`CSid`物件或`SID`運算子左邊的結構是否大於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。|
|[operator <=](#operator_lt__eq)|測試是否`CSid`物件或`SID`運算子左邊的結構是否小於或等於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。|
|[operator >=](#operator_gt__eq)|測試是否`CSid`物件或`SID`運算子左邊的結構是否大於或等於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。|

## <a name="requirements"></a>需求

**標頭：** atlsecurity.h。

##  <a name="operator_eq_eq"></a>  運算子 = =

比較`CSid`物件或`SID`結構是否相等的 （安全性識別碼）。

```
bool operator==(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

為 true，則傳回的物件是否相等，FALSE 如果不相等。

##  <a name="operator_neq"></a>  運算子 ！ =

比較`CSid`物件或`SID`結構是否不相等的 （安全性識別碼）。

```
bool operator==(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

為 true，則傳回的物件是否不相等，如果相等，則為 FALSE。

##  <a name="operator_lt"></a>  運算子 <

測試是否`CSid`物件或`SID`運算子左邊的結構是小於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。

```
bool operator<(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

如果為 true 的地址*lhs*物件是否小於一個的位址*rhs*物件，FALSE 否則。

### <a name="remarks"></a>備註

此運算子處理程式碼的地址`CSid`物件或`SID`結構，並實作以提供與相容性C++標準程式庫集合類別。

##  <a name="operator_gt"></a>  operator >

測試是否`CSid`物件或`SID`運算子左邊的結構是否大於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。

```
bool operator<(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

如果為 true 的地址*lhs*大於的地址*rhs*，否則為 FALSE 否則。

### <a name="remarks"></a>備註

此運算子處理程式碼的地址`CSid`物件或`SID`結構，並實作以提供與相容性C++標準程式庫集合類別。

##  <a name="operator_lt__eq"></a>  運算子 < =

測試是否`CSid`物件或`SID`運算子左邊的結構是否小於或等於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。

```
bool operator<(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

如果為 true 的地址*lhs*小於或等於的地址*rhs*，否則為 FALSE 否則。

### <a name="remarks"></a>備註

此運算子處理程式碼的地址`CSid`物件或`SID`結構，並實作以提供與相容性C++標準程式庫集合類別。

##  <a name="operator_gt__eq"></a>  operator >=

測試是否`CSid`物件或`SID`運算子左邊的結構是否大於或等於`CSid`物件或`SID`右側的結構 (如C++標準程式庫相容性)。

```
bool operator<(const CSid& lhs, const CSid& rhs) throw();
```

### <a name="parameters"></a>參數

*lhs*<br/>
第一個`CSid`物件或`SID`来比較的結構。

*rhs*<br/>
第二個`CSid`物件或`SID`来比較的結構。

### <a name="return-value"></a>傳回值

如果為 true 的地址*lhs*大於或等於的地址*rhs*，否則為 FALSE 否則。

### <a name="remarks"></a>備註

此運算子處理程式碼的地址`CSid`物件或`SID`結構，並實作以提供與相容性C++標準程式庫集合類別。
