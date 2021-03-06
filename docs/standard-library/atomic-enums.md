---
title: '&lt;atomic&gt; 列舉'
ms.date: 11/04/2016
f1_keywords:
- atomic/std::memory_order
ms.assetid: cd3a81c5-a19e-448f-952a-c34c717f21a9
helpviewer_keywords:
- std::memory_order
ms.openlocfilehash: 03247f6abd01b00fbbed3b33016cd4a12d8a13f8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62377282"
---
# <a name="ltatomicgt-enums"></a>&lt;atomic&gt; 列舉

## <a name="memory_order_enum"></a> memory_order 列舉

為記憶體位置上的同步處理作業提供符號名稱。 這些作業會影響一個執行緒的指派如何在其他執行緒中變成可見。

```cpp
typedef enum memory_order {
    memory_order_relaxed,
    memory_order_consume,
    memory_order_acquire,
    memory_order_release,
    memory_order_acq_rel,
    memory_order_seq_cst,
} memory_order;
```

### <a name="enumeration-members"></a>列舉型別成員

|||
|-|-|
|`memory_order_relaxed`|不需要任何順序。|
|`memory_order_consume`|載入作業做為記憶體位置上的消耗行為。|
|`memory_order_acquire`|載入作業做為記憶體位置上的取得行為。|
|`memory_order_release`|儲存作業做為記憶體位置上的釋放作業。|
|`memory_order_acq_rel`|合併 `memory_order_acquire` 與 `memory_order_release`。|
|`memory_order_seq_cst`|合併 `memory_order_acquire` 與 `memory_order_release`。 標記為 `memory_order_seq_cst` 的記憶體存取必須是循序一致。|

## <a name="see-also"></a>另請參閱

[\<atomic>](../standard-library/atomic.md)<br/>
