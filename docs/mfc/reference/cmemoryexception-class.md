---
title: CMemoryException 類別
ms.date: 11/04/2016
f1_keywords:
- CMemoryException
- AFX/CMemoryException
- AFX/CMemoryException::CMemoryException
helpviewer_keywords:
- CMemoryException [MFC], CMemoryException
ms.assetid: 9af0ed57-d12a-45ca-82b5-c910a60f7edf
ms.openlocfilehash: 11be0eba080085c507ed718ea23219ca1c93aeba
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64341172"
---
# <a name="cmemoryexception-class"></a>CMemoryException 類別

表示記憶體不足例外狀況。

## <a name="syntax"></a>語法

```
class CMemoryException : public CSimpleException
```

## <a name="members"></a>成員

### <a name="public-constructors"></a>公用建構函式

|名稱|描述|
|----------|-----------------|
|[CMemoryException::CMemoryException](#cmemoryexception)|建構 `CMemoryException` 物件。|

## <a name="remarks"></a>備註

沒有進一步限定性條件是必要或不可能。 會自動擲回記憶體例外狀況**新**。 如果您撰寫您自己的記憶體函式，使用`malloc`，範例中，則您必須負責擲回記憶體例外狀況。

如需詳細資訊`CMemoryException`，請參閱文章[例外狀況處理 (MFC)](../../mfc/exception-handling-in-mfc.md)。

## <a name="inheritance-hierarchy"></a>繼承階層

[CObject](../../mfc/reference/cobject-class.md)

[CException](../../mfc/reference/cexception-class.md)

[CSimpleException](../../mfc/reference/csimpleexception-class.md)

`CMemoryException`

## <a name="requirements"></a>需求

**標頭：** afx.h

##  <a name="cmemoryexception"></a>  CMemoryException::CMemoryException

建構 `CMemoryException` 物件。

```
CMemoryException();
```

### <a name="remarks"></a>備註

請勿直接使用這個建構函式，但而不是呼叫全域函式[AfxThrowMemoryException](exception-processing.md#afxthrowmemoryexception)。 此全域函式會在記憶體不足的情況下成功，因為它是由建構先前配置的記憶體中的例外狀況物件。 如需例外狀況處理的詳細資訊，請參閱文章[例外狀況](../exception-handling-in-mfc.md)。

## <a name="see-also"></a>另請參閱

[CException 類別](cexception-class.md)<br/>
[階層架構圖表](../hierarchy-chart.md)
