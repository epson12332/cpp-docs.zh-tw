---
title: C 後置遞增和遞減運算子
ms.date: 11/04/2016
helpviewer_keywords:
- increment operators, syntax
- scalar operators
- types [C], scalar
ms.assetid: 56ba218d-65f9-405f-8684-caccc0ca33aa
ms.openlocfilehash: 8c2e3ba50ce3e768b377a588cd3e82ad29df79ee
ms.sourcegitcommit: f4be868c0d1d78e550fba105d4d3c993743a1f4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56150633"
---
# <a name="c-postfix-increment-and-decrement-operators"></a>C 後置遞增和遞減運算子

後置遞增和遞減運算子的運算元是可修改左值的純量類型。

## <a name="syntax"></a>語法

*postfix-expression*：<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*postfix-expression*  **++**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*postfix-expression*  **--**

後置遞增或遞減運算的結果為運算元的值。 取得結果之後，運算元的值會遞增 (或遞減)。 下列程式碼示範後置遞增運算子。

```
if( var++ > 0 )
    *p++ = *q++;
```

在此範例中，變數 `var` 會與 0 相比，然後再遞增。 如果 `var` 在遞增前是正數，則會執行下一個陳述式。 首先會將 `q` 所指向的物件值指派給 `p` 所指向的物件。 然後再將 `q` 和 `p` 遞增。

## <a name="see-also"></a>另請參閱

[後置遞增和遞減運算子：++ 和 --](../cpp/postfix-increment-and-decrement-operators-increment-and-decrement.md)
