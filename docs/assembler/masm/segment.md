---
title: SEGMENT
ms.date: 08/30/2018
f1_keywords:
- SEGMENT
helpviewer_keywords:
- SEGMENT directive
ms.assetid: e6f68367-6714-4f06-a79c-edfa88014430
ms.openlocfilehash: f37be47b92a71e20821cd1e40f8cf1350dfedaff
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62210371"
---
# <a name="segment"></a>SEGMENT

定義呼叫的程式區段*名稱*區段屬性

## <a name="syntax"></a>語法

> *name* SEGMENT [[READONLY]] [[*align*]] [[*combine*]] [[*use*]] [[*characteristics*]] ALIAS(*string*) [['*class*']]<br/>
> *statements*<br/>
> *名稱*結束

#### <a name="parameters"></a>參數

*align*<br/>
可從中選取區段的起始位址的記憶體位址範圍。 對齊類型可以是下列其中一項動作：

|對齊類型|起始位址|
|----------------|----------------------|
|**BYTE**|下一個可用的位元組位址。|
|**WORD**|下一個可用的字位址 （每個字的 2 個位元組）。|
|**DWORD**|下一個可用的雙精度浮點數字位址 （每個雙字組 4 個位元組）。|
|**PARA**|下一個可用的段落位址 （每個段落的 16 位元組）。|
|**PAGE**|下一個可用的頁面位址 （每一頁的 256 個位元組）。|
|**ALIGN**(*n*)|下一個可用*n*個位元組的位址。 如需詳細資訊，請參閱 < 備註 > 一節。|

如果未指定此參數，**並行**預設會使用。

*combine*<br/>
**公用**，**堆疊**，**常見**，**記憶體**，**在**<em>位址</em>， **私用**

*use*<br/>
**USE16**， **USE32**，**一般**

*characteristics*<br/>
**INFO**，**閱讀**，**撰寫**， **EXECUTE**，**共用**， **NOPAGE**， **NOCACHE**，和**捨棄**

這些只支援 COFF，並對應至 COFF 區段的特性相似的名稱 (例如**共用**對應至 IMAGE_SCN_MEM_SHARED)。 讀取設定 IMAGE_SCN_MEM_READ 旗標。 過時的唯讀旗標會造成要清除 IMG_SCN_MEM_WRITE 旗標的區段。 如果有的話*特性*設定，不會使用預設的特性，而且只有程式設計師指定旗標作用中。

`ALIAS(` *字串* `)`<br/>
這個字串做為發出 COFF 物件中的區段名稱。  建立多個區段具有相同的外部名稱，具有相異的 MASM 區段名稱。

不支援使用 **/omf**。

*class*<br/>
指定應該如何組合和排列組合的檔案中的區段。 典型值為， `'DATA'`， `'CODE'`，`'CONST'`和 `'STACK'`

## <a name="remarks"></a>備註

針對`ALIGN(n)`， *n*可以是任何 2 的乘冪從 1 到 8192; 不支援 **/omf**。

## <a name="see-also"></a>另請參閱

[指示詞參考](../../assembler/masm/directives-reference.md)<br/>