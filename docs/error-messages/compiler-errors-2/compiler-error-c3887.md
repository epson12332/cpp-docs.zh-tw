---
title: 編譯器錯誤 C3887
ms.date: 11/04/2016
f1_keywords:
- C3887
helpviewer_keywords:
- C3887
ms.assetid: a7e82426-ef99-437b-9562-2822004e18fe
ms.openlocfilehash: 85434cb8daba0db82843c09e2d1bb09d98960272
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "64344508"
---
# <a name="compiler-error-c3887"></a>編譯器錯誤 C3887

'var': 常值資料成員初始設定式必須是常數運算式

A[常值](../../extensions/literal-cpp-component-extensions.md)資料成員只能使用常數運算式初始化。

下列範例會產生 C3887:

```
// C3887.cpp
// compile with: /clr
ref struct Y1 {
   static int i = 9;
   literal
   int staticConst = i;   // C3887
};
```

可能的解決方式：

```
// C3887b.cpp
// compile with: /clr /c
ref struct Y1 {
   literal
   int staticConst = 9;
};
```