---
title: CFixedStringT 類別
ms.date: 03/27/2019
f1_keywords:
- CFixedStringT
- CSTRINGT/ATL::CFixedStringT
- CSTRINGT/ATL::CFixedStringT::CFixedStringT
helpviewer_keywords:
- CFixedStringT class
- shared classes, CFixedStringT
ms.assetid: 6d4171ba-3104-493a-a6cc-d515f4ba9a4b
ms.openlocfilehash: 6c7649b7131e3b1620112acf89867d0731d7265d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62235157"
---
# <a name="cfixedstringt-class"></a>CFixedStringT 類別

此類別代表固定的字元緩衝區的字串物件。

## <a name="syntax"></a>語法

```
template<class StringType, int t_nChars>
class CFixedStringT : private CFixedStringMgr, public StringType
```

#### <a name="parameters"></a>參數

*StringType*<br/>
用於固定的字串物件的基底類別，而且可以是任何`CStringT`-基底類型。 部分範例包括`CString`， `CStringA`，和`CStringW`。

*t_nChars*<br/>
儲存在緩衝區中的字元數。

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CFixedStringT::CFixedStringT](#cfixedstringt)|字串物件的建構函式。|

### <a name="public-operators"></a>公用運算子

|名稱|描述|
|----------|-----------------|
|[CFixedStringT::operator =](#operator_eq)|指派新值到`CFixedStringT`物件。|

## <a name="remarks"></a>備註

此類別為基礎的自訂字串類別的範例`CStringT`。 雖然相似，但這兩個類別有不同的實作。 之間的主要差異`CFixedStringT`和`CStringT`是：

- 初始字元的緩衝區配置物件的一部分，而且大小*t_nChars*。 這可讓`CFixedString`佔用連續記憶體區塊，基於效能用途的物件。 不過，如果內容`CFixedStringT`超過下列大小時物件*t_nChars*，緩衝區會以動態方式配置。

- 字元緩衝區`CFixedStringT`物件永遠都是相同的長度 ( *t_nChars*)。 上的緩衝區大小沒有限制`CStringT`物件。

- Memory manager`CFixedStringT`使共用的自訂[CStringData](../../atl-mfc-shared/reference/cstringdata-class.md)之間兩個或多個物件`CFixedStringT`不允許的物件。 `CStringT` 物件不需要這項限制。

如需有關自訂`CFixedStringT`和字串物件的記憶體管理一般情況下，請參閱 <<c2> [ 記憶體管理和 CStringT](../../atl-mfc-shared/memory-management-with-cstringt.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

`IAtlStringMgr`

`StringType`

`CFixedStringMgr`

`CFixedStringT`

## <a name="requirements"></a>需求

**標頭：** cstringt.h

##  <a name="cfixedstringt"></a>  CFixedStringT::CFixedStringT

建構 `CFixedStringT` 物件。

```
CFixedStringT() throw();
explicit CFixedStringT(IAtlStringMgr* pStringMgr) throw();
CFixedStringT(const CFixedStringT<StringType, t_nChars>& strSrc);
CFixedStringT(const StringType& strSrc);
CFixedStringT(const StringType::XCHAR* pszSrc);
explicit CFixedStringT(const StringType::YCHAR* pszSrc);
explicit CFixedStringT(const unsigned char* pszSrc);
```

### <a name="parameters"></a>參數

*pszSrc*<br/>
要複製到這個 null 結尾字串`CFixedStringT`物件。

*strSrc*<br/>
將現有`CFixedStringT`要複製到這個物件`CFixedStringT`物件。

*pStringMgr*<br/>
指向的記憶體管理員的`CFixedStringT`物件。 如需詳細資訊`IAtlStringMgr`和 記憶體管理`CFixedStringT`，請參閱[記憶體管理和 CStringT](../../atl-mfc-shared/memory-management-with-cstringt.md)。

### <a name="remarks"></a>備註

因為建構函式會將輸入的資料複製到新配置的儲存體，您應該注意可能會造成例外狀況，該記憶體。 部分這些建構函式做為轉換函式。

##  <a name="operator_eq"></a>  CFixedStringT::operator =

重新初始化現有`CFixedStringT`物件的新資料。

```
CFixedStringT<StringType, t_nChars>& operator=(
    const CFixedStringT<StringType, t_nChars>& strSrc);
CFixedStringT<StringType, t_nChars>& operator=(const char* pszSrc);
CFixedStringT<StringType, t_nChars>& operator=(const wchar_t* pszSrc);
CFixedStringT<StringType, t_nChars>& operator=(const unsigned char* pszSrc);
CFixedStringT<StringType, t_nChars>& operator=(const StringType& strSrc);
```

### <a name="parameters"></a>參數

*pszSrc*<br/>
要複製到這個 null 結尾字串`CFixedStringT`物件。

*strSrc*<br/>
將現有`CFixedStringT`複製到這個`CFixedStringT`物件。

### <a name="remarks"></a>備註

您應該注意可能會發生例外狀況，每當您使用指派運算子，因為新的儲存體通常配置來保存所產生的記憶體`CFixedStringT`物件。

## <a name="see-also"></a>另請參閱

[CStringT 類別](../../atl-mfc-shared/reference/cstringt-class.md)<br/>
[階層架構圖表](../../mfc/hierarchy-chart.md)<br/>
[ATL/MFC 共用類別](../../atl-mfc-shared/atl-mfc-shared-classes.md)
