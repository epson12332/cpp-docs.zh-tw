---
title: /LINKERMEMBER
ms.date: 11/04/2016
f1_keywords:
- /linkermember
helpviewer_keywords:
- /LINKERMEMBER dumpbin option
- LINKERMEMBER dumpbin option
- -LINKERMEMBER dumpbin option
ms.assetid: c96868c1-d70e-4651-ae36-c55b58b16406
ms.openlocfilehash: a0456fd9ed1729b4a6cfa200a54ba211a64e94ea
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62216580"
---
# <a name="linkermember"></a>/LINKERMEMBER

```
/LINKERMEMBER[:{1|2}]
```

## <a name="remarks"></a>備註

此選項會顯示在文件庫中定義的公用符號。 請指定 1 個引數以顯示符號順序物件，以及它們的位移。 指定顯示位移與物件的索引數目的 2 個引數，然後再清單依字母順序排列的順序，以及每個物件索引中的符號。 若要取得這兩個輸出，請指定 /LINKERMEMBER 沒有數字的引數。

只有[/HEADERS](headers.md) DUMPBIN 選項只適用於所產生的檔案上[/GL](gl-whole-program-optimization.md)編譯器選項。

## <a name="see-also"></a>另請參閱

[DUMPBIN 選項](dumpbin-options.md)
